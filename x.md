The Pallets Projects
Projects
Governance
People
Blog
Donate
Blog
Categories
Meta
Releases
Security
Blog Feed
New Major Versions Released! Flask 2.0, Jinja 3.0, Click 8.0, Werkzeug 2.0, ItsDangerous 2.0, and MarkupSafe 2.0
written by David Lord on 2021-05-11 in Releases

The Pallets team is pleased to announce that the next major versions for our six core projects have been released!

This represents two years of work by the Pallets team and community, there are a significant number of changes and exciting new features. Check out the logs for every project to see what's new. Flask depends on the five other libraries, be sure to read them all if you're upgrading Flask.

Flask 2.0
Jinja 3.0
Click 8.0
Werkzeug 2.0
ItsDangerous 2.0
MarkupSafe 2.0
Installing and Upgrading
Install from PyPI with pip. For example, for Flask:

pip install -U Flask
The projects have all dropped support for Python 2 and 3.5, requiring Python 3.6 as the minimum supported version. We plan to follow CPython's supported versions as our supported versions.

Some less common parts of the projects, or parts that we've determined are better served by external implementations, have been deprecated. Previously deprecated code has also been removed. Testing tools such as pytest enable showing deprecation warnings automatically, and can turn them into errors so that you can see early what you may need to change in your project.

While we strive to avoid compatibility issues, there may turn out to be incompatibilities either directly or through other dependencies your project uses, such as Flask extensions. Over the next few weeks, the ecosystem around our projects will continue to update to improve compatibility as necessary. We encourage you to use tools such as pip-compile and Dependabot to pin and control upgrades to your dependencies to avoid unexpected changes.

Renaming the Default Branch
We are joining the PSF, CPython, and Django, among many other projects, in renaming the default branch of our repositories to "main". GitHub makes this transition easy, see their documentation about how it works for maintainers and users.

If you have a local copy of the repository you'll need to rename its branch to "main".

$ git branch -m master main
$ git fetch origin
$ git branch -u origin/main main
$ git remote set-head origin -a
If you were installing from a GitHub archive URL such as https://github.com/pallets/flask/archive/refs/heads/master.zip, you'll need to rename that link to use "main".

Release Highlights
These are a few of the great new features and changes to be aware of in the projects. Check out the linked changelogs for the full lists of changes.

All Projects
Support Python 3.6 and above only. Removing the compatibility code makes the code faster, as well as easier to maintain and contribute to.
Comprehensive type annotations have been added to the code. This makes type checking your own code more useful, and allows IDEs to provide better completion and help.
Use tools such as pre-commit, black, flake8, and pyupgrade to ensure the code and new PRs follow the same style consistently.
Flask 2.0
Support async views and other callbacks such as error handlers, defined with async def. Regular sync views continue to work unchanged. ASGI features such as web sockets are not supported. We will continue exploring how to add more support for async.
Blueprints can be nested under other blueprints, allowing a more layered approach to organizing the application.
Add route decorators for common HTTP API methods. For example, @app.post("/login") is a shortcut for @app.route("/login", methods=["POST"]).
Better CLI errors when an app could not be loaded. Running the development server shows errors immediately, they are only deferred on reloads.
A new Config.from_file function to load config from any file format.
The flask shell command enables tab completion like the regular python shell does.
When serving static files, browsers will cache based on content rather than a 12 hour timer. This means changes to static content such as CSS styles will be reflected immediately on reload without needing to clear the cache.
Werkzeug 2.0
Parsing multipart/form-data has been optimized and shows a 15x speedup, especially for large file uploads.
Locals use Python's ContextVar to allow working across async coroutines instead of only threads.
All request and response code has been merged into single classes instead of composing multiple mixin classes.
While this is not a public API yet, the Request and Response classes are becoming sans-io. This will allow us to better support sync and async use cases in the future.
The test client always returns a Response class that includes a reference to the original request, environ, and any redirects that were followed.
datetime objects returned by some headers and functions are timezone-aware.
URL routing understands ws:// and wss:// schemes and will route appropriately. While there is no direct support for websockets, this allows other projects to use Werkzeug's routing.
Move Flask's implementation of send_file and send_from_directory to Werkzeug.
The debugger no longer uses jQuery, which significantly reduces the size of the package.
The reloader is smarter about watching or ignoring directories.
The development server avoids showing 0.0.0.0 and warns about not running in production.
Colors are shown correctly in the server log on Windows.
Jinja 3.0
Async environments and rendering no longer requires patching. This feature will continue to be improved now that async is natively supported.
Blocks can be marked as required.
Variables set in blocks or loops can be accessed in context functions, as well as inner scoped blocks. Macros have access to the current template globals.
Filters and tests used within if blocks and ternary statements can be undefined at runtime. Tests have been added to check if a filter or test is available, to allow optionally using them.
I18N supports pgettext and npgettext.
NativeEnvironment supports enable_async mode.
Click 8.0
The shell tab completion system has been completely rewritten. It now allows every command, group, parameter, and type to provide custom completion, supports sending metadata such as the type to the shell for better native support, and provides a way to add support for new shells.
style supports 256 and RGB color codes supported by modern terminals, as well as the strikethrough, italic, and overline styles.
New class attributes make it easier to customize the core objects.
The context can manage resources that use context managers across commands. For example, this makes it easier to manage a database connection.
Options with multiple=True or nargs don't require setting a default, and properly validate the format of a default if it's given.
Options can be used as only a flag to use a default value, or prompt for a value only if the flag is given.
Prompts validate using the option's custom callback in addition to its type.
Help formatting and short help message generate has been improved.
Command line arguments on Windows support glob patterns like *.txt and ~/config.json, since the Windows terminal does not support this automatically.
Messages shown to users, such as validation and errors, are marked as I18N translatable with gettext.
ItsDangerous 2.0
Added support for key rotation by passing a list of valid keys instead of a single key.
datetime objects are timezone-aware.
MarkupSafe 2.0
Wheels are provided for 33 Python version / OS / architecture combinations, to make installing with speedups easy. Newly added are ManyLinux 2014 and OSX Universal 2 wheels.
Follow and Get Involved
Follow our blog RSS feed or our Twitter @PalletsTeam to get future updates. We also have an official Discord server https://discord.gg/pallets for chatting, asking questions, and contributing to the projects.

If you're interested in contributing, each project has a guide showing how to get started with a development environment and the tools we use. Check out the issue trackers for each project for what to work on. Use the Watch feature on GitHub see new issues, PRs, and the discussions we have around them.

Donate to Support Our Work
The Pallets organization accepts donations as part of the non-profit Python Software Foundation (PSF). Donations through the PSF support our efforts to maintain the projects and grow the community.

Click here to donate. ❤

For Enterprise
The Pallets team and thousands of other packages are working with Tidelift to deliver commercial support and maintenance for the open source dependencies you use to build your applications. Save time, reduce risk, and improve code health, while paying the maintainers of the exact dependencies you use.

Learn more.

Thank You!
We've made amazing progress, both by working through the backlog of issues and PRs, as well as growing the team and community. We have so many more exciting things in store. Look for more updates soon on community projects such as documentation translations and FlaskCon Online 2021! Thank you so much for using, supporting, and contributing to the Pallets projects!

   License & Copyright • Contact • Made with  and Lektor • Powered by Netlify