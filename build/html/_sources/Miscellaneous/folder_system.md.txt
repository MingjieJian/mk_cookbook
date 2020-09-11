# "Standard" folder system

From [here](https://stackoverflow.com/questions/22842691/what-is-the-meaning-of-the-dist-directory-in-open-source-projects).

- `src/`: "source" files to build and develop the project. This is where the original source files are located, before being compiled into fewer files to dist/, public/ or build/.
- `dist/`: "distribution", the compiled code/library, also named public/ or build/. The files meant for production or public use are usually located here.
- `assets/`: static content like images, video, audio, fonts etc.
- `lib/`: external dependencies (when included directly).
- `test/`: the project's tests scripts, mocks, etc.
- `node_modules/`: includes libraries and dependencies for JS packages, used by Npm.
- `vendor/`: includes libraries and dependencies for PHP packages, used by Composer.
- `bin/`: files that get added to your PATH when installed.

The folders used often are `src/`, `dist/`, `assets/` and `bin/`.