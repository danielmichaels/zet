# WGD Fri 2022-06-10


## [Storeman](https://github.com/danielmichaels/storeman)

Started on a project for cataloguing my many storage boxes and their contents using QR codes.

Its a pretty simple premise, instead of writing or using your memory, you'll put a QR code
on a storage container. The QR links to a page with a list of its contents including
images for future reference. I'm writing it in Go using basic templates and a little
bit of [Alpine.js](https://alpinejs.dev).

We've moved across three states and four homes in the last four years. Moving sucks but
not knowing what's in the many boxes we have laying around the garage sucks even more.

- Scaffolded basic structure
- Created database layer and migrations
- Views for home and viewing containers done at a basic level
- Templating and form helpers integrated into the Server struct

Authentication and session management is up next

## Misc 

- Landed a new lease, moving in at the end of the month. 
- Bought a nice second hand car to replace our old one - makes getting to work a lot easier
- Deployed my own [PicoShare](https://github.com/mtlynch/picoshare) instance at [share.danielms.site](https://share.danielms.site) using [fly](https://fly.io).
