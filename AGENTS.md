# AGENT

about me and the way i like code

- i love clean consistent code
- i care about the small details
- i like haveing comments like this ```// ==============```, after the import statemnets at the top of the file and at the bottom of the file, i like there to be enough = to be ablout the leanght of the first line, and every single one of those comments must be the exact same leanght everywhere in a project.
- i like less than 100 lines of code per a file if we can, and clear names, and ussually one function per a file.
- i like clear_snake_case for all functions and consts, can be lowwercase or ALL_CAPS, when ever you see something not in this case fix it.
- all things must end with what they are this_does_this_fun, for functions, and _const for const, or _interface for interfcae, matching the case of what ever so if we have and all caps stuct NETWORK_ID_STRUCT, it silly that i have to say this, but one time agent did lowercase append what it was when the rest was all caps
- i hate js comments with /* for muliti line, just use two //
- for ts web apps i like bun and rsbuild and svelte
- for web apps i like clean consol loging for things just for the sake of having consol loging, but not to much, like consol loging for data fetching, and the data, but not for user navigation actions
- as with comments in my code conslo logs shoul have ```======``` on both sides the smae length as they are everywhere else for that particlar projct.
- another thing i mentioned a few things that need to be consistent per project, tjough i will try to be conssistent with all projects, the big thing is that all the code in a project is consistent
- i run "bunx prettier . --write" and "cargo fmt" to make sure code it formated right, this i do myself do not run for me. just make sure you are wrting code that is formated clean.
- please run typecheck or cargo check after adding code or feature, and then if it is a web app i am usly runing myself so you do not have to run. i usully do not like to run a build command to verify that yes it still comiles but whatever is best, ussuly nice to see that it builds. i like runing something to verify it works, so if fast scipt that does something run it, if it is a long runing scipt timeout run it so you dont just watch it stream data forever.


---

#### README's

i like my project readem's to follow a very specific formate, simple and cosise, see example readme's
- [README.example.bun.md](./README.example.bun.md), this is an example for a package, if it was a web app would be almost the smae but web specif bun run dev like commands in the dev section and no how to use section. if a package and constain another md file on how to use or whaytever, but not in main reame one add line is all i want there.
- [README.example.rust.md](./README.example.rust.md), sample for Dioxus web app.

the main project read me should be consise and have nothing more or less than these examples.

can create specif consise .md files for other things like RUN.md DOCKER.MD, and everything should have it's own readme like every compose file, but don't get to carried away.

---

copyright 2026 by sleet.near