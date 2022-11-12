# The F2E 2022 W1


### **UI design from [EG](https://2022.thef2e.com/users/12061549261454740203)**　　**UI 設計稿來自 [EG](https://2022.thef2e.com/users/12061549261454740203)**


## [DEMO](https://aa367421.github.io/F2E_2022_W1/index.html)（https://aa367421.github.io/F2E_2022_W1/index.html）


## Work Description 作品說明


The F2E 2022 第一關的作品，感謝有這個機會讓我能用 GSAP 實作滾動視差相關的技術

也再次感謝 [EG](https://2022.thef2e.com/users/12061549261454740203) 大神的設計稿，第一眼就被吸引了，想說多看幾件作品再決定，最後還是回來到這份設計稿

在實作時實作到動物們衝線的那剎那也覺得自己衝線了（然而還有平板和手機的 RWD 在前方……）

不論如何，最後都還是獻出了肝臟完成了，明天的我值得一頓好吃的！


## Project Description 系統說明


專案部分沒有額外用 npm 等方式引入套件，套件和外部CSS都是直接以 CDN 方式引入


## Folder Description 資料夾說明

* resource : [EG](https://2022.thef2e.com/users/12061549261454740203) 提供的圖片、以及部分由自己拼接而成（ bg 裡的 bg_talking.png ）
* js : JavaScript 檔案們
* sass : sass 檔案們
* css : sass 編譯過後的 css 檔案們

* 檔案名稱：
  - entryDivertion : 負責剛進入畫面的階段，包括整體的初始化、 loading 頁面、游標圖示等
  - allForDesktop : 桌機端的 js / sass / css 們
  - allForNotDesktop : 平板、手機等 max-width <= 820px 裝置的 桌機端的 js / sass / css 們


## Technology & Library 使用技術

* Normalize CSS
* SASS
* GSAP 、 ScrollTrigger
  - 主要的動態達成
* jQuery
  - Scroll to top 的部分


## Other and Features 其他想說的話與記給自己的一些特別花時間的技術點

一開始實作時，桌機端部分的動態主要採用 GSAP 的 timeline 物件達成，但實作到中途才發現 SrollTrigger 的 scrub 不該打開，導致 timeline 裡每個動態的比例都超小而且超難控管……

也因為這樣，桌機端的 sass 裡幾乎都直接把元素釘死，後來做平板、手機端時心一橫直接重開了一個檔案，後續再由 JS 在讀取時動態判斷、載入不同的 css 檔來處理

平板和手機端的動態做得就有比較讓自己滿意了，也更單純好寫好讀！（技術文件要看清楚的悲痛……），不過桌機端的 JS 就成了一坨 .to 的義大利麵…… feel so sorry...

### Loading Page 讀取頁面

主要有關 entryDivertion.js 和 entryDivertion.css

JS 部分，假讀取用 GSAP 達成，原本監聽讀取完畢的事件是抓 window.onload ，後來發現抓互動元素（\_h、\_p等等）的 preload 完成點會讓使用體驗好上許多，後來決定用這個方式

小插曲是原本沒有想寫動態載入 CSS 檔，原本想說可能 JS 動態載入就是極限了，只能對肝臟說抱歉……，然後又為了動態載入 CSS 後的重新渲染把 loading 監聽的邏輯反反覆覆地改，最後才定案呈現在這樣，用 `getDevice()` 抓 `clientWidth` 判斷裝置（有覺得應該血更嚴謹，但時間和肝臟所迫，這次主要研究的東西還是放在動態），再監聽後續的 preload 完成事件


CSS 部分，讀取完成的圓形遮罩困擾許久，後來用 CSS 的 clip-path 和 opacity 搭配 GSAP 完成，不過這樣的方法需要固定 container 的寬高，如果使用者是在網頁中途重新整理的話，圓形遮罩會在不理想的位置出現（這樣的方法也沒辦法讓 container 是 fixed 的），後來在 JS 部分多寫 `scrollY != 0` 才跑圓形遮罩和淡入的動態

如果下次有類似的動態需要執行，也許可以試試看在 container 裡多蓋一層元素來解決？現在 container 同時作為 viewport 的狀況下，好像暫時沒辦法用這樣的方法破解（或有沒有機會 clip-path 有反向剪裁能用呢……

### 桌機端的角色動態

主要有關 entryDivertion.js 中約 59 行左右開始的 `device == 'desktop'` 判斷裡的游標移動監聽，也包含了游標圖示更換

角色動態部分，因為隨著區塊不同，動物被套用不同的 scale ，所以用了 `getLeaderAnimal()` 抓三個動物的高度來判斷誰處於領先，在後續的游標監聽中就讓他和其他兩隻動物移動反方向，營造視覺的錯落感。主要實現方式則是取游標的 x 值，對三隻動物做對應的 translateX 移動

在區塊轉換時會因為 `getLeaderAnimal()` 的改變所以導致動物瞬間移動，這部分如果下次還有需要處理，可能要想想怎麼把它變得更流暢或是用其他方式實現


## [DEMO](https://aa367421.github.io/F2E_2022_W1/index.html)（https://aa367421.github.io/F2E_2022_W1/index.html）


### **UI design from [EG](https://2022.thef2e.com/users/12061549261454740203)**　　**UI 設計稿來自 [EG](https://2022.thef2e.com/users/12061549261454740203)**


from 2022/11/08 - 2022/11/12

