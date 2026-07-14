Build a Flutter App

See also: [[wedsite_tools/techstack/Flutter]] · [[building a Frontend]] · [[building a Backend]] · [[Web Tools MOC]]

```cmd
# check environment
flutter doctor

# create project (org reverse-domain แนะนำใช้ com.company.app)
flutter create --org com.apexcore my_app
cd my_app

# state mgmt + routing + DI
flutter pub add flutter_riverpod riverpod_annotation go_router get_it injectable

# network + local storage
flutter pub add dio shared_preferences hive hive_flutter flutter_secure_storage flutter_dotenv

# model / codegen
flutter pub add freezed_annotation json_annotation

# UI utils
flutter pub add intl cached_network_image flutter_svg google_fonts

# dev deps
flutter pub add -d build_runner riverpod_generator freezed json_serializable injectable_generator flutter_lints mocktail

# run codegen
dart run build_runner build --delete-conflicting-outputs

# run app
flutter run
```

Build release:
```cmd
flutter build apk --release
flutter build appbundle --release
flutter build ios --release
flutter build web --release
```

Flavors (dev/prod):
```cmd
flutter run --flavor dev -t lib/main_dev.dart
flutter run --flavor prod -t lib/main_prod.dart
```

---

pubspec.yaml (ส่วนสำคัญ)
```yaml
name: my_app
description: Enterprise Flutter application.
publish_to: 'none'
version: 1.0.0+1

environment:
  sdk: '>=3.3.0 <4.0.0'

dependencies:
  flutter:
    sdk: flutter
  flutter_riverpod: ^2.5.1
  go_router: ^14.2.0
  get_it: ^7.7.0
  injectable: ^2.4.2
  dio: ^5.5.0
  shared_preferences: ^2.2.3
  hive_flutter: ^1.1.0
  flutter_secure_storage: ^9.2.2
  flutter_dotenv: ^5.1.0
  freezed_annotation: ^2.4.4
  json_annotation: ^4.9.0
  intl: ^0.19.0
  cached_network_image: ^3.3.1
  google_fonts: ^6.2.1

dev_dependencies:
  flutter_test:
    sdk: flutter
  build_runner: ^2.4.11
  riverpod_generator: ^2.4.0
  freezed: ^2.5.7
  json_serializable: ^6.8.0
  injectable_generator: ^2.6.1
  flutter_lints: ^4.0.0
  mocktail: ^1.0.4

flutter:
  uses-material-design: true
  assets:
    - assets/images/
    - assets/icons/
    - .env
  fonts:
    - family: Poppins
      fonts:
        - asset: assets/fonts/Poppins-Regular.ttf
        - asset: assets/fonts/Poppins-Bold.ttf
          weight: 700
```

analysis_options.yaml
```yaml
include: package:flutter_lints/flutter.yaml

linter:
  rules:
    prefer_const_constructors: true
    prefer_single_quotes: true
    always_declare_return_types: true
    avoid_print: true
```

lib/main.dart
```dart
import 'package:flutter/material.dart';
import 'package:flutter_dotenv/flutter_dotenv.dart';
import 'package:flutter_riverpod/flutter_riverpod.dart';
import 'package:hive_flutter/hive_flutter.dart';

import 'app.dart';
import 'core/di/injection.dart';

Future<void> main() async {
  WidgetsFlutterBinding.ensureInitialized();

  await dotenv.load(fileName: '.env');
  await Hive.initFlutter();
  configureDependencies(); // get_it + injectable

  runApp(const ProviderScope(child: MyApp()));
}
```

lib/app.dart
```dart
import 'package:flutter/material.dart';
import 'package:flutter_riverpod/flutter_riverpod.dart';

import 'core/router/app_router.dart';
import 'core/theme/app_theme.dart';

class MyApp extends ConsumerWidget {
  const MyApp({super.key});

  @override
  Widget build(BuildContext context, WidgetRef ref) {
    final router = ref.watch(appRouterProvider);

    return MaterialApp.router(
      title: 'My App',
      debugShowCheckedModeBanner: false,
      theme: AppTheme.light,
      darkTheme: AppTheme.dark,
      routerConfig: router,
    );
  }
}
```

lib/core/router/app_router.dart (go_router)
```dart
import 'package:flutter_riverpod/flutter_riverpod.dart';
import 'package:go_router/go_router.dart';

import '../../features/auth/presentation/pages/login_page.dart';
import '../../features/home/presentation/pages/home_page.dart';

final appRouterProvider = Provider<GoRouter>((ref) {
  return GoRouter(
    initialLocation: '/login',
    routes: [
      GoRoute(path: '/login', builder: (context, state) => const LoginPage()),
      GoRoute(path: '/home', builder: (context, state) => const HomePage()),
    ],
    redirect: (context, state) {
      // TODO: ตรวจสอบ auth state แล้ว redirect
      return null;
    },
  );
});
```

lib/core/network/dio_client.dart
```dart
import 'package:dio/dio.dart';
import 'package:flutter_dotenv/flutter_dotenv.dart';

class DioClient {
  final Dio dio;

  DioClient()
      : dio = Dio(
          BaseOptions(
            baseUrl: dotenv.env['API_BASE_URL'] ?? '',
            connectTimeout: const Duration(seconds: 15),
            receiveTimeout: const Duration(seconds: 15),
          ),
        ) {
    dio.interceptors.add(
      InterceptorsWrapper(
        onRequest: (options, handler) {
          // TODO: แนบ token จาก secure storage
          handler.next(options);
        },
        onError: (error, handler) {
          // TODO: จัดการ 401 -> refresh token / logout
          handler.next(error);
        },
      ),
    );
  }
}
```

lib/core/di/injection.dart (get_it + injectable)
```dart
import 'package:get_it/get_it.dart';
import 'package:injectable/injectable.dart';

import 'injection.config.dart';

final getIt = GetIt.instance;

@InjectableInit()
void configureDependencies() => getIt.init();
```

Feature module example — Auth (Clean Architecture)
```dart
// domain/repositories/auth_repository.dart
abstract class AuthRepository {
  Future<UserEntity> login(String email, String password);
}

// domain/usecases/login_usecase.dart
class LoginUseCase {
  final AuthRepository repository;
  LoginUseCase(this.repository);

  Future<UserEntity> call(String email, String password) {
    return repository.login(email, password);
  }
}

// data/repositories/auth_repository_impl.dart
class AuthRepositoryImpl implements AuthRepository {
  final AuthRemoteDataSource remote;
  AuthRepositoryImpl(this.remote);

  @override
  Future<UserEntity> login(String email, String password) async {
    final model = await remote.login(email, password);
    return model.toEntity();
  }
}

// presentation/providers/auth_provider.dart
final authControllerProvider =
    AsyncNotifierProvider<AuthController, UserEntity?>(AuthController.new);

class AuthController extends AsyncNotifier<UserEntity?> {
  @override
  Future<UserEntity?> build() async => null;

  Future<void> login(String email, String password) async {
    state = const AsyncLoading();
    state = await AsyncValue.guard(
      () => getIt<LoginUseCase>().call(email, password),
    );
  }
}
```

.env
```
API_BASE_URL=https://api.example.com
API_KEY=changeme
```

.gitignore (Flutter เฉพาะ)
```
.env
.dart_tool/
.flutter-plugins
.flutter-plugins-dependencies
build/
**/*.g.dart
**/*.freezed.dart
**/injection.config.dart
```
