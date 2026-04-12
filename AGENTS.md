# AGENT

about me and the way i like code

- i love clean consistent code
- i care about the small details
- i like having comments like this ```// ==============```, after the import statements at the top of the file and at the bottom of the file, i like there to be enough = to be about the length of the first line, and every single one of those comments must be the exact same length everywhere in a project.
- i like less than 100 lines of code per a file if we can, and clear names, and usually one function per a file.
- i like clear_snake_case for all functions and consts, can be lowercase or ALL_CAPS, whenever you see something not in this case fix it.
- all things must end with what they are this_does_this_fun, for functions, and _const for const, or _interface for interface, matching the case of whatever so if we have an all caps struct NETWORK_ID_STRUCT, it is silly that i have to say this, but one time agent did lowercase append what it was when the rest was all caps
- i hate js comments with /* for multi line, just use two //
- for ts web apps i like bun and rsbuild and svelte
- for web apps i like clean console logging for things just for the sake of having console logging, but not too much, like console logging for data fetching, and the data, but not for user navigation actions
- as with comments in my code console logs should have ```======``` on both sides the same length as they are everywhere else for that particular project.
- another thing i mentioned a few things that need to be consistent per project, though i will try to be consistent with all projects, the big thing is that all the code in a project is consistent
- i run "bunx prettier . --write" and "cargo fmt" to make sure code it formatted right, this i do myself do not run for me. just make sure you are writing code that is formatted clean.
- please run typecheck or cargo check after adding code or feature, and then if it is a web app i am usually running myself so you do not have to run. i usually do not like to run a build command to verify that yes it still compiles but whatever is best, usually nice to see that it builds. i like running something to verify it works, so if a fast script that does something run it, if it is a long running script timeout run it so you don't just watch it stream data forever.


---

#### README's

- i like my project readme's to follow a very specific format, simple and concise, see example readme's
- [README.example.bun.md](./README.example.bun.md), this is an example for a package, if it was a web app, it would be almost the same but web specific bun run dev like commands in the dev section and no how to use section. if a package can contain another md file on how to use or whatever, but not in main readme one add line is all i want there.
- [README.example.rust.md](./README.example.rust.md), sample for Dioxus web app.

the main project readme should be concise and have nothing more or less than these examples.

can create specific concise .md files for other things like RUN.md DOCKER.MD, and everything should have it's own readme like every compose file, but don't get too carried away.

---

copyright 2026 by sleet.near