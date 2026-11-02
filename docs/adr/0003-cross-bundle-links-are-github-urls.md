# Cross-bundle links are GitHub URLs to main

Links between bundles use GitHub URLs pointing at the target concept's `main` (`https://github.com/<org>/<repo>/blob/main/okf/<concept>.md`); links within a bundle use bundle-relative `/...` paths. We chose URLs over relative filesystem paths because the bundles are separate repositories, and relative paths only resolve while all worktrees are checked out side by side — they break the moment a single bundle is read on its own.
