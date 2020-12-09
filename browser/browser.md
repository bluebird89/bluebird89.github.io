# Brower

* [beaker](https://beakerbrowser.com/):Beaker is a peer-to-peer browser with tools to create and host websites.
* Google 基于Webkit
* Safari Webkit内核
* Firefox自研Gecko内核
  - 像JavaScript引发的alert窗口或file组件打开的窗口，都属于模态窗口，它们会阻塞所有主线程中正在执行的JavaScript代码
* Edge
* [browsershots](http://browsershots.org/)
* [brave-browser](https://github.com/brave/brave-browser):Brave browser for Desktop and Laptop computers running Windows, OSX, and Linux <https://www.brave.com>
* beaker
* Opera
  - adds unlimited VPN service to its
* [qutebrowser](https://www.qutebrowser.org)
* [Tor](http://torproject.lu/)
* vivaldi
* [Onion]=(https://onionbrowser.com/)
  - [](https://tor-browser.en.softonic.com/mac)
  - [Deep](https://github.com/mr-likar/DeepWeb)
* [Nessie](https://www.radsix.com/) an extremely simple web browser for Windows

```
curl -s https://brave-browser-apt-release.s3.brave.com/brave-core.asc | sudo apt-key --keyring /etc/apt/trusted.gpg.d/brave-browser-release.gpg add -

echo "deb [arch=amd64] https://brave-browser-apt-release.s3.brave.com/ stable main" | sudo tee /etc/apt/sources.list.d/brave-browser-release.list

sudo apt update

sudo apt install brave-browser
```

## 功能

* 右侧的➕，可以生成 PWA

## [Bookmarklets](https://www.ph-uhl.com/0010-Bookmarklets/)

* Like a tiny Add-on for your browser. You drag it into your bookmark-bar and when you click it, it does something

## 工具

* [browsh](https://github.com/browsh-org/browsh):A fully-modern text-based browser, rendering to TTY and browsers <https://www.brow.sh>
* [push.js](https://github.com/Nickersoft/push.js):The world's most versatile desktop notifications framework 🌎 <https://pushjs.org>
* [CodeMirror](https://github.com/codemirror/CodeMirror):In-browser code editor <http://codemirror.net/>
* [xterm.js](https://github.com/xtermjs/xterm.js):A terminal for the web <https://xtermjs.org/>
* [OctoLinker](OctoLinker/OctoLinker):OctoLinker – Available on Chrome, Firefox and Opera <https://octolinker.github.io>
* [muon](https://github.com/brave/muon):Build browsers and browser like applications with HTML, CSS, and JavaScript <https://discord.gg/TcT5tX2w>
* [KodExplorer](https://github.com/kalcaddle/KodExplorer):A web based file manager,web IDE / browser based code editor <http://kodcloud.com>
* [browser-sync](https://github.com/BrowserSync/browser-sync):Keep multiple browsers & devices in sync when building websites. <http://browsersync.io>
* [floccus](https://github.com/marcelklehr/floccus):Sync your bookmarks across browsers via Nextcloud, WebDAV or a local file (and thus any file sync solution)

## 参考

* [浏览器的工作原理：新式网络浏览器幕后揭秘](https://www.html5rocks.com/en/tutorials/internals/howbrowserswork/)
