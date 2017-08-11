# refresh-develop
refreshes firefox on file changes (developping)

When you develop web apps you need to view changes so you save the file move to the web browser and then refresh the web browser.

This script makes things a lot easier. It uses inotify-tools and netcat and it need the firefox addon: remote-control, get it from this link: https://addons.mozilla.org/en-US/firefox/addon/remote-control/

## How to use?

1. add remote-control plugin to firefox https://addons.mozilla.org/en-US/firefox/addon/remote-control/

2. install **inotify-tools**

3. install **netcat**

4. open *~/.bashrc* and paste the following:

`function roc() { echo reload | nc -c localhost 32000; };
function odc() { while true; do inotifywait $(find . -type d); roc; done; }`

5. `source ~/.bashrc`

6. open a new tab in the terminal, `cd` to the directory that contains web files and run `odc`

7. open the page in the browser (and activate the addon)

## further options:

you can sync a folder with your local host folder with the following additional steps:

- install **async**

- modify what you have pasted in *~/.bashrc* accordingly:

`function roc() { sudo rsync -avz --delete . /opt/lampp/htdocs/; echo reload | nc -c localhost 32000; };
function odc() { while true; do inotifywait $(find . -type d); roc; done; }`

## A video for demonstration:

[![Video Demonstration](https://img.youtube.com/vi/yhwZXId6jvM/0.jpg)](https://www.youtube.com/watch?v=yhwZXId6jvM) 
