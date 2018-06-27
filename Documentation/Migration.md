# Migration

Pointers for migration between major versions.

## Upgrading to 4.0

- Make sure you use Swift 4 / Xcode 9 since we've adjusted to the syntax and SDK changes.
- Running R.swift now requires the `generate` command, check the error R.swift outputs for upgrade instructions
- Capitalization of methods and properties might have changed, in these cases the compiler should generate a fix-it for you.
- Support for CLR-files is deprecated, use the new named Color assets instead where possible.
 * CLR based colors are moved from `R.color.*` to `R.clr.*`
 * Support for CLR files will be removed in a later version
- At the moment we are compatible with both Swift 3.2 and Swift 4, this is more an accident then a feature, beware that we might drop Swift 3.2 support anytime.
- If you upgrade from Swift 2 we advise you to first migrate to Swift 3 / R.swift 3.0 and when that is done apply the migration to Swift 4 / R.swift 4.0

## Upgrading to 3.0

- Make sure you use Swift 3 / Xcode 8 since we've adjusted to the syntax changes.
- If you want to use Swift 2.3 / Xcode 8 use the latest R.swift 2 release.
- Some methods are renamed to match the new Swift 3 naming conventions, there are annotations available so the compiler can help you migrate.

## Upgrading to 2.0

- Make sure you use Swift 2.2 / Xcode 7.3 since we've adjusted to the syntax changes.

## Upgrading to 1.0

- iOS 7 support is dropped, use [R.swift 0.13](https://github.com/mac-cain13/R.swift/releases/tag/v0.13.0) if you still have to support it.
- Generated code now depends on the [R.swift.Library](https://github.com/mac-cain13/R.swift.Library), CocoaPods users don't need to do anything. Manual installation users need to include this library themselves, see the readme for instructions.
- In general; properties that created new stuff are now functions to represent better that they actually create a new instance.
 * `R.image.settingsIcon` changed to  `R.image.settingsIcon()`
 * `R.file.someJson` changed to `R.file.someJson()`
 * `R.storyboard.main.initialViewController` changed to `R.storyboard.main.initialViewController()`
 * `R.storyboard.main.someViewController` changed to `R.storyboard.main.someViewController()`
- In general; Where you needed to use `.initialize()` to get the instance, a shorter function is available now:
 * `R.storyboard.main.initialize()` changed to `R.storyboard.main()`
 * `R.nib.someView.initiate()` changed to `R.nib.someView()`
- Nib root view loading changed from `R.nib.someView.firstView(nil, options: nil)` to `R.nib.someView.firstView(owner: nil)`
- Typed segue syntax changed from `segue.typedInfoWithIdentifier(R.segue.someViewController.someSegue)` to `R.segue.someViewController.someSegue(segue: segue)`
- Runtime validation changed:
 * `R.validate()` now throws errors it encounters
 * `R.assertValid()` asserts on errors and only performs action in a debug/non-optimized build
 * For regular use cases using `R.assertValid()` is recommended
