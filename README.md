## 機器人說明

### FB Bot Framework

參考 [FB Messenger Platform](https://developers.facebook.com/docs/messenger-platform/implementation#send_message)

### 功能類別

1. Web Plugins

有兩種類別Plugins可以放在網站(desktop web and mobile web)．其中一種是Send To Messenger可以帶一個訊息送到聊天室, 另外一種叫做Message Us,則是開啟與我們的聊天室．在Desktop web, 是開啟Messenger.com. 而在Mobile web則會嘗試開啟Messenger native app.

![Facebook Web Plugins ](https://scontent-tpe1-1.xx.fbcdn.net/t39.2178-6/12995596_1049096845170018_1587653123_n.png)

2. Customer Matching

這項功能則是允許當你擁有顧客的手機號碼與他們希望你能聯絡他們的時候，你可以透過這項功能用bot與這些顧客互動(意味不一定需要透過顧客的fb_id就能與顧客互動)

![Facebook Customer Matching](https://scontent-tpe1-1.xx.fbcdn.net/t39.2178-6/12995553_268475126826430_1088661696_n.png)

3. Bot

可以讓每個人開發Bot在messager串接，最大好處是可以把對話資料都收下來．有兩個大問題1. 收到的顧客messenger id不等於他們的Facebook id 2. 我們沒有他們的email.

 ![Your Bot in Messenger](https://scontent-tpe1-1.xx.fbcdn.net/t39.2178-6/12995608_262382634098427_340178745_n.png)
 
 
 4. Messenger Codes and Links
 
 一個FB自己的掃碼連結到專業Messager
 
 
  ![Messenger Codes and Links](https://scontent-tpe1-1.xx.fbcdn.net/v/t1.0-9/12963404_1296845976998228_789563813989987883_n.jpg?oh=9fab596c5feb490807fa5bda9a2990c6&oe=57DCEFE9)
  
  
  ### Features in a Conversation
  
  1. *Welcome Screen (歡迎畫面)
  當顧客第一次來到這個粉絲專頁Messager會看見的話, 與Bot無關，就只是設定．但這是審核必有的項目 
  
    ![Welcome Screen](https://scontent-tpe1-1.xx.fbcdn.net/t39.2178-6/12995546_473451206187753_917419200_n.png)
    
  
  2. Structured Templates 結構化對話
  
  有許多種對話方式, 有簡單回話,圖文,圖文加單一按鈕,有回傳測定參數多按鈕(call-to-action)
  
   ![Structured Templates 1](https://scontent-tpe1-1.xx.fbcdn.net/t39.2178-6/12679454_1026083487461743_881543663_n.png)
 
 ![Structured Templates ](https://scontent-tpe1-1.xx.fbcdn.net/t39.2178-6/12995543_192638781122814_2026367341_n.png)
 
 3. User Controls (使用者控制項)
 
 FB會持續提供更多項目，讓顧客可以透過對話與店家互動
 
  ![User Controls ](https://scontent-tpe1-1.xx.fbcdn.net/t39.2178-6/12057143_198218393902993_755928037_n.png)
  
  
  
  
  
### 發送訊息

- Text and Image Messages
單純文字或圖片
  
![Text and Image Messages ](https://scontent-tpe1-1.xx.fbcdn.net/t39.2178-6/12532937_1707565839531937_1916590448_n.png)

- Structured Messages
結構化選項與圖文，同時裡面可以加上call-to-action或者是open URL
   
![Structured Messages 1](https://scontent-tpe1-1.xx.fbcdn.net/t39.2178-6/12679454_228093174215421_635988637_n.png)

![Structured Messages 2](https://scontent-tpe1-1.xx.fbcdn.net/t39.2178-6/12995563_1711733995711442_1886079481_n.png)
  
- Inbox vs Message Requests
可以讓訊息出現在inbox或者是Message Request提醒顧客
  
![Inbox vs Message Requests](https://scontent-tpe1-1.xx.fbcdn.net/t39.2178-6/12601315_1703870573235346_288847799_n.png)


### Send/Receive API (訊息收發API)

- User IDs
一旦拿到**pages_messaging**的權限，，就能透過顧客的user_id發送訊息給他們，但這個id是根據專頁走的，並不是顧客真的的Facebook id,所以如果真的需要連結兩邊，需要自己在透過一些額外的手法進行連結

- Phone Numbers (Customer Matching)
一旦拿到 **pages_messaging_phone_number**，就能利用他們的電話號碼發送訊息給他們,而這個權限就不一定需要顧客要有第一次的與我們的facebook專頁互動就能直接發送訊息給他們,主動性更強!
但除非他們願意與這個專頁的bot開啟第一次互動，不然一樣都無法拿到顧客的相關資訊．
此外這個功能必須專頁要是在美國或者是有一個管理者是在美國

- Request

    - Text and Image Messages
    - Structured Messages
      - Button Template
      - Generic Template, including imsage, title,subtitle, description, and buttons.
      - Receipt Template

- Response
    
    - recipient_id 專頁id
    - message_id 訊息id
    
- Delivery Receipts
透過Rest回傳資訊可以知道訊息已經發送了，但一定要有** message_deliveries**權限

- Postback Callbacks
透過**messaging_postbacks**權限，可以讓顧客點擊具有回送特定訊息的按鈕後，把該訊息提供給bot

- Welcome Screen (給第一次與專頁溝通使用）
- Messenger Greeting (每次開啟與顧客溝通使用)
- User Profile API
參考
     https://graph.facebook.com/v2.6/<USER_ID>?fields=first_name,last_name,profile_pic,locale,timezone,gender&access_token=<PAGE_ACCESS_TOKEN>