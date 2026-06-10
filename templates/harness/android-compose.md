## Project Harness — Android (Jetpack Compose + MVI + Hilt)

### Stack
- Language: Kotlin 2.0
- UI Framework: Jetpack Compose (BOM 2024.06)
- Dependency Injection: Hilt
- Architecture: MVI (Model-View-Intent)
- State management: StateFlow
- Navigation: Lambda callbacks passed to composables
- Async: Kotlin Coroutines + Flow
- Networking: Retrofit + OkHttp
- Local storage: Room
- Image loading: Coil

### Conventions

**ViewModel**
- Exposes: `uiState: StateFlow<ScreenUiState>`
- UiState is a sealed interface with at minimum: `Idle`, `Loading`, `Error`
- One-shot events sent via `Channel<UiEvent>` consumed as `Flow`
- Domain layer uses `Result<T>` or sealed classes — never raw exceptions

**Composables**
- Receive state + callbacks only — no direct ViewModel reference
- Navigation via lambda callbacks (e.g. `onLoginSuccess: () -> Unit`)
- `@Preview` required for each state variant (Idle, Loading, Error)

**Naming**
- Screens: `<Feature>Screen.kt`
- ViewModels: `<Feature>ViewModel.kt`
- UiState: `<Feature>UiState`
- UiEvents: `<Feature>UiEvent`
- Hilt modules: `<Feature>Module.kt`
- Test files: `<Feature>ViewModelTest.kt`
- Test methods: `givenX_whenY_thenZ`

**Strings**
- All user-facing strings via `stringResource(R.string.id)`
- Never hardcode strings in composables

### Test framework
- Unit tests: JUnit 5 + MockK + Turbine (for Flow testing)
- UI tests: Compose Testing (ComposeTestRule)
- Assertions: AssertK or JUnit 5 built-in

### Avoid
- LiveData (use StateFlow)
- XML Views (Compose only)
- Material2 imports (Material3 only)
- `viewModelScope.launch` inside composables
- Hardcoded strings (use `stringResource`)
- Exposing domain exceptions directly to UI layer
- NavController references inside ViewModel
- Business logic inside composables
- `runBlocking` outside of tests
