# Agent instructions for this iOS repository

Copy this file to the root of your repository, fill in the brackets, and commit it. Codex reads `AGENTS.md`; Claude Code reads `CLAUDE.md`, which can point here with a single line: `@AGENTS.md`.

## Project

- Open: `[App.xcworkspace or App.xcodeproj]`
- App scheme: `[App]`
- Test plan or test scheme: `[AppTests]`
- Minimum iOS version: `[17.0]`
- Dependencies: `[Swift Package Manager | CocoaPods: run pod install first]`

## How to prove a change

1. Build for an iOS Simulator with the app scheme. A change is not done until it builds.
2. Run the tests that cover the change, then the full suite before opening a pull request.
3. For any change a user can see, launch the app on a Simulator and attach a screenshot of each changed screen to the pull request.
4. Put derived data, result bundles and screenshots under `.build/`, which is ignored by git.

The `ios-build-and-test` skill in [macswarm/ios-agent-kit](https://github.com/macswarm/ios-agent-kit) has the exact commands.

## Working next to other agents

Several agents may share this Mac, each in its own git worktree.

- Work only inside your worktree. Do not edit files in another agent's worktree or in the main checkout.
- Do not erase or shut down Simulators you did not boot. Uninstall your app to reset state instead.
- Builds may queue. Do not cancel another agent's `xcodebuild`.
- Commit and push before you finish. Uncommitted work may be lost when the machine is recycled.

## Do not

- Change signing settings, provisioning profiles or the team ID.
- Commit secrets, `.xcresult` bundles, `DerivedData` or Simulator screenshots outside the paths the reviewer asked for.
- Upgrade Xcode, Swift tools versions or package major versions unless the task asks for it.
