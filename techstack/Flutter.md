See also: [[building a Flutter]] · [[React.js]] · [[Next.js]] · [[Web Tools MOC]]

> ### 🚀 Tools Used
Flutter (Framework) + Dart (Language)
Google's UI toolkit for building natively compiled apps for mobile, web, and desktop from a single codebase.
👉 Get Started with Flutter – [flutter.dev](https://docs.flutter.dev/get-started/install)

---

### Installation

Check environment (SDK, platform toolchains, IDE plugins):
```bash
flutter doctor

flutter run -d chrome
```

Create a new Flutter app:
```bash
flutter create my_app
cd my_app
flutter run
```

Recommended packages (state mgmt, routing, network, DI):
```bash
# state management
flutter pub add flutter_riverpod riverpod_annotation

# routing
flutter pub add go_router

# networking / API
flutter pub add dio retrofit

# local storage
flutter pub add shared_preferences hive hive_flutter flutter_secure_storage

# dependency injection
flutter pub add get_it injectable

# model / json serialization
flutter pub add json_annotation freezed_annotation

# utils / UI
flutter pub add intl flutter_svg cached_network_image google_fonts

# dev dependencies (codegen, lint, testing)
flutter pub add -d build_runner riverpod_generator freezed json_serializable
flutter pub add -d flutter_lints mocktail
```

Run code generation (freezed / json_serializable / injectable / riverpod_generator):
```bash
dart run build_runner build --delete-conflicting-outputs

# watch mode while developing
dart run build_runner watch --delete-conflicting-outputs
```

---

### Flutter Project Full Structure

Clean Architecture · Feature-first · Riverpod + go_router

```
my_app/
├── android/                          # Native Android project
├── ios/                              # Native iOS project
├── web/                              # Web target (ถ้า build for web)
├── macos/ windows/ linux/            # Desktop targets (ถ้าต้องการ)
│
├── assets/                           # Static assets ที่ pubspec.yaml ต้อง declare
│   ├── images/
│   │   ├── logo.png
│   │   └── banner.png
│   ├── icons/
│   │   └── app_icon.svg
│   ├── fonts/
│   │   └── Poppins-Regular.ttf
│   └── lang/                         # ไฟล์แปลภาษา (i18n)
│       ├── en.json
│       └── th.json
│
├── lib/
│   ├── main.dart                     # Entry point (เรียก runApp)
│   ├── main_dev.dart                 # Entry point แยกตาม flavor (optional)
│   ├── main_prod.dart
│   ├── app.dart                      # Root widget (MaterialApp.router + Theme)
│   │
│   ├── core/                         # โค้ดกลางที่ใช้ร่วมกันทั้งแอป
│   │   ├── constants/
│   │   │   ├── app_colors.dart
│   │   │   ├── app_strings.dart
│   │   │   └── app_sizes.dart
│   │   ├── theme/
│   │   │   ├── app_theme.dart
│   │   │   ├── text_styles.dart
│   │   │   └── app_theme_extension.dart
│   │   ├── router/
│   │   │   ├── app_router.dart       # go_router configuration
│   │   │   └── route_names.dart
│   │   ├── network/
│   │   │   ├── dio_client.dart       # ตั้งค่า Dio + interceptors
│   │   │   ├── api_endpoints.dart
│   │   │   └── network_exceptions.dart
│   │   ├── error/
│   │   │   ├── failure.dart          # Failure classes (Freezed)
│   │   │   └── exceptions.dart
│   │   ├── usecase/
│   │   │   └── usecase.dart          # Base UseCase<Type, Params>
│   │   ├── di/
│   │   │   ├── injection.dart        # get_it + injectable setup
│   │   │   └── injection.config.dart # generated
│   │   ├── utils/
│   │   │   ├── validators.dart
│   │   │   ├── formatters.dart
│   │   │   ├── logger.dart
│   │   │   └── extensions/
│   │   │       ├── context_extension.dart
│   │   │       └── string_extension.dart
│   │   └── widgets/                  # Widget กลางที่ใช้ซ้ำได้ทั้งแอป
│   │       ├── app_button.dart
│   │       ├── app_text_field.dart
│   │       ├── loading_indicator.dart
│   │       ├── error_view.dart
│   │       └── empty_state.dart
│   │
│   ├── features/                     # แยกตาม feature (feature-first)
│   │   ├── auth/
│   │   │   ├── data/
│   │   │   │   ├── datasources/
│   │   │   │   │   ├── auth_remote_datasource.dart
│   │   │   │   │   └── auth_local_datasource.dart
│   │   │   │   ├── models/
│   │   │   │   │   └── user_model.dart       # freezed + json_serializable
│   │   │   │   └── repositories/
│   │   │   │       └── auth_repository_impl.dart
│   │   │   ├── domain/
│   │   │   │   ├── entities/
│   │   │   │   │   └── user_entity.dart
│   │   │   │   ├── repositories/
│   │   │   │   │   └── auth_repository.dart  # abstract interface
│   │   │   │   └── usecases/
│   │   │   │       ├── login_usecase.dart
│   │   │   │       ├── register_usecase.dart
│   │   │   │       └── logout_usecase.dart
│   │   │   └── presentation/
│   │   │       ├── providers/
│   │   │       │   └── auth_provider.dart    # Riverpod (StateNotifier/AsyncNotifier)
│   │   │       ├── pages/
│   │   │       │   ├── login_page.dart
│   │   │       │   └── register_page.dart
│   │   │       └── widgets/
│   │   │           ├── login_form.dart
│   │   │           └── social_login_buttons.dart
│   │   │
│   │   ├── home/
│   │   │   ├── data/
│   │   │   ├── domain/
│   │   │   └── presentation/
│   │   │       ├── providers/
│   │   │       ├── pages/
│   │   │       │   └── home_page.dart
│   │   │       └── widgets/
│   │   │
│   │   ├── dashboard/
│   │   │   ├── data/
│   │   │   ├── domain/
│   │   │   └── presentation/
│   │   │       ├── pages/
│   │   │       │   ├── dashboard_page.dart
│   │   │       │   └── settings_page.dart
│   │   │       └── widgets/
│   │   │
│   │   └── profile/
│   │       ├── data/
│   │       ├── domain/
│   │       └── presentation/
│   │
│   ├── l10n/                         # Localization (intl / ARB files)
│   │   ├── app_en.arb
│   │   └── app_th.arb
│   │
│   └── shared/                       # Model/enum ที่ใช้ข้าม feature
│       ├── models/
│       │   └── paginated_response.dart
│       └── enums/
│           └── request_state.dart
│
├── test/                             # Unit / widget tests
│   ├── features/
│   │   └── auth/
│   │       ├── data/
│   │       ├── domain/
│   │       └── presentation/
│   ├── core/
│   └── helpers/
│       └── test_helper.dart
│
├── integration_test/                 # Integration / e2e tests
│   └── app_test.dart
│
├── .env / .env.dev / .env.prod       # Environment variables (flutter_dotenv)
├── .gitignore
├── analysis_options.yaml             # Lint rules (flutter_lints)
├── pubspec.yaml                      # Dependencies + assets declaration
├── pubspec.lock
├── build.yaml                        # build_runner config (optional)
└── README.md
```

---

### Layer Responsibility (Clean Architecture)

| Layer | Responsibility |
|---|---|
| **presentation/** | UI (Widgets, Pages) + State (Riverpod Providers) — no business logic |
| **domain/** | Entities, Repository interfaces, UseCases — pure Dart, no Flutter/package deps |
| **data/** | Repository implementation, DataSources (remote/local), Models (DTO ↔ Entity mapping) |
| **core/** | Cross-cutting concerns: routing, theming, DI, network client, error handling |

Data flow: `UI → Provider → UseCase → Repository (interface) → RepositoryImpl → DataSource → API/DB`
