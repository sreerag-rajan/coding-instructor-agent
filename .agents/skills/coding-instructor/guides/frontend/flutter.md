# Flutter Frontend Guide

## Phase 1 — Language Foundation Concept Priorities (Dart)

| Lesson | Key Concepts to Cover | DSA Task Patterns |
|--------|----------------------|-------------------|
| Hello World | `main()`, `print()`, `dart run`, variables, `var`/`final`/`const` | — |
| Data Types | `int`, `double`, `String`, `bool`, `null`, null safety (`?`, `!`), `dynamic` | Type conversion, string interpolation |
| Collections | `List<T>`, `Map<K,V>`, `Set<T>`, collection if/for/spread | Frequency counting, grouping, deduplication |
| Control Flow | `if/else`, `for`, `for-in`, `while`, `switch`, `break`/`continue` | Iteration, pattern generation |
| Functions | Named parameters, positional params, arrow syntax, anonymous functions | Utility functions |
| Classes & OOP | `class`, constructor, `this`, named constructors, `extends`, `implements`, `mixin`, `abstract` | Model entities |
| DSA Fundamentals | Recursion, sorting with `List.sort()`, searching | Implement linked list, binary search |

## Phase 2 — Frontend Domain (13 Lessons)

| # | Lesson | Key Concepts | Framework Nuances | Testing |
|---|--------|-------------|-------------------|---------|
| 8 | Framework Setup & First Render | `flutter create`, `MaterialApp`, `Scaffold`, `runApp()`, default counter app, hot reload | Widget tree. `runApp(MyApp())`. `MaterialApp` with `home:`. Default page renders | `flutter test`: `widgetTest(() { ... })`. Framework-provided test passes |
| 9 | First Page — Content Only | Clear template, `Text` widget, `Image.network()` placeholder, `TextStyle`, `AppBar`, widget tree composition | Replace `MyHomePage` content. `Scaffold(body: Center(child: Column(children: [...])))` | `widgetTest`: `find.text('expected text')`. Check heading `TextStyle` |
| 10 | Layouts & Alignment | `Row`, `Column`, `Expanded`, `Flexible`, `GridView.count`, `SizedBox`, `MainAxisAlignment`, `CrossAxisAlignment` | `GridView.count(crossAxisCount: 4)` for body. Footer as `Row` with 3 `Expanded` children | `widgetTest`: check grid children count. Check layout structure |
| 11 | Responsive Design | `LayoutBuilder`, `MediaQuery`, `OrientationBuilder`, breakpoints (width-based), adaptive layouts, responsive grid columns | `LayoutBuilder(builder: (ctx, constraints) { ... })`. Change grid `crossAxisCount` based on width | Test with different screen sizes. Use `MediaQuery` override in test. Check column count changes |
| 12 | Theming & Color Systems | `ThemeData`, `Theme` widget, `Theme.of(context)`, `ThemeData.light()`/`dark()`, custom `ColorScheme`, design tokens | `ThemeData` in `MaterialApp(themeMode:, theme:, darkTheme:)`. Theme toggle with state | `pumpWidget` with theme override. Check `Theme.of(context)` values. Toggle theme |
| 13 | Complex UI Components | `DataTable`, `ExpansionTile` (accordion), `TabBar` + `TabBarView` (tabs), `Card` widget, list rendering | `DefaultTabController`, `TabBar`, `TabBarView`. `ExpansionTile` for accordion. `DataTable` with `DataColumn`, `DataRow` | `widgetTest`: tab switches, expansion tile toggles, table has rows. Scroll tests if needed |
| 14 | Routing & Navigation | `Navigator.push`, `MaterialPageRoute`, named routes (`routes:`), `onGenerateRoute`, `Navigator.pop`, `pushReplacement`, 404 | Named routes in `MaterialApp(routes: {})`. `Navigator.pushNamed('/about')`. `unknownRoute:` for 404 | `widgetTest` with `MaterialApp` wrapper. Pump with initial route. Test navigation |
| 15 | Component Modularization | Extract custom widgets: `AppCard`, `AppAccordion`, `AppDataTable`. Constructor parameters. Separate files in `widgets/` dir | StatelessWidget with constructor params. Composition: `Widget Function` builder or `child:` | `widgetTest` each widget. Check different param combinations. Test composition |
| 16 | Dynamic Forms | `Form` widget, `TextFormField`, `DropdownButtonFormField`, `CheckboxListTile`, `validator`, `FormState`, dynamic field generation | `Form(key: _formKey)`. Build fields from List<FieldDef>. `onSaved` for each. `_formKey.currentState!.save()` | Fill form, submit, check `onSaved` values. Test validation errors. Reset |
| 17 | Mock API Integration | `http`/`dio` package, `mockito`/`mocktail`, repository pattern, `FutureBuilder` or state management, loading/error/empty/success states | Abstract repository interface → mock implementation. `ChangeNotifier` or `FutureBuilder` for UI states | `mockito` stub returning different states. `pumpWidget` + verify UI. Test all 4 states |
| 18 | Global State Management | `Provider` (`ChangeNotifierProvider`) or `Riverpod`, state notifier, `context.watch`/`context.read`, cross-page state sharing | Provider: `MultiProvider` wrapping app. `ChangeNotifier` with `notifyListeners()`. Theme state in provider | ProviderScope in tests. Test state changes. Verify widgets rebuild on state change |
| 19 | Advanced Components (Modals, Animations) | `showDialog`, `AlertDialog`, custom dialog widget, `AnimatedContainer`, `AnimatedOpacity`, `PageRouteBuilder` for transitions, modal focus | `showDialog(context: context, builder: ...)`. `AnimatedContainer` for smooth property transitions | `pumpAndSettle` for animations. Test dialog appears/disappears. Check modal barrier click |
| 20 | Capstone — Full App | Combines: routing, Provider/Riverpod, mock API, dynamic form, modal modals, responsive, theming, custom widgets. 3+ screens | Feature folder structure (`screens/`, `widgets/`, `models/`, `providers/`). All states handled | `integration_test` for full flows. widgetTest per feature. Test navigation through all screens |

## ⚠️ Important

Phase 1 must be taught in plain Dart files (`.dart`). Phase 2 introduces Flutter widgets and Material Design. Emphasize the "widget tree" mental model early.

## Recommended Setup

- **Flutter SDK** (latest stable)
- **Provider** (simpler, official) or **Riverpod** (more powerful, testable)
- **mockito** or **mocktail** for API mocking
- **go_router** or standard Navigator for routing

## Testing

Framework: `flutter_test` (built-in) with `widgetTest`, `integration_test` for full flow tests.