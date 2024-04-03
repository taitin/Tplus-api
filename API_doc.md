# T-Plus 內部 API 文件

## 文件目的

- 本文檔定義網站 API 進出參規範,並提供範例格式.

## 傳輸規範

- 使用 TPC/IP 作為傳輸層協議
- 使用 HTTP 作為應用層協議
- 上傳參數用 multipart/form-data
- 回應參數格式皆為 json
- 此接口清單遵循 restful 設計理念

## 接口說明

### API 網址

- 測試機網址

### [HTTP 接口清單](#http接口)

### 常用回傳參數說明

#### Course

| 名稱       | 類型   | 說明                  | 範例                  |
| :--------- | :----- | :-------------------- | :-------------------- |
| id         | int    | 課堂 ID               | 6                     |
| user_id    | int    | 老師 User ID          | 2                     |
| class_name | string | 班級名稱              | "一年三班"            |
| subject    | string | 科目名稱              | "英文"                |
| code       | string | 課堂碼                | "BpQYoYzMZm"          |
| is_open    | int    | 開課狀態              | 0                     |
| status     | string | 課堂狀態 (string)     | "qa"                  |
| status_id  | int    | 課堂狀態相關 ID (int) | 1                     |
| qrcode_svg | string | 課堂 QRCode svg       | 參考下方 json         |
| created_at | string | 建立時間              | "2023-12-29 20:48:18" |
| updated_at | string | 更新時間              | "2023-12-29 20:48:18" |
| deleted_at | string | 刪除時間              | "2023-12-29 20:48:18" |
| user       | json   | 課堂老師資料          | 參考下方 user         |

qrcode_svg

```json
"<?xml version=\"1.0\" encoding=\"UTF-8\"?>\n<svg xmlns=\"http://www.w3.org/2000/svg\" version=\"1.1\" width=\"100\" height=\"100\" viewBox=\"0 0 100 100\"><rect x=\"0\" y=\"0\" width=\"100\" height=\"100\" fill=\"#ffffff\"/><g transform=\"scale(4.762)\"><g transform=\"translate(0,0)\"><path fill-rule=\"evenodd\" d=\"M10 0L10 1L11 1L11 0ZM12 0L12 2L13 2L13 0ZM8 2L8 3L9 3L9 2ZM10 2L10 3L11 3L11 2ZM12 3L12 4L11 4L11 5L10 5L10 4L9 4L9 6L8 6L8 8L4 8L4 9L3 9L3 8L0 8L0 11L2 11L2 12L0 12L0 13L2 13L2 12L3 12L3 13L8 13L8 17L9 17L9 18L8 18L8 21L10 21L10 20L11 20L11 21L12 21L12 20L14 20L14 21L21 21L21 20L20 20L20 19L21 19L21 18L20 18L20 17L19 17L19 18L20 18L20 19L19 19L19 20L14 20L14 19L17 19L17 18L16 18L16 16L12 16L12 17L11 17L11 16L10 16L10 14L11 14L11 13L12 13L12 12L13 12L13 13L14 13L14 11L12 11L12 9L13 9L13 10L14 10L14 9L15 9L15 11L19 11L19 12L18 12L18 13L17 13L17 12L15 12L15 13L16 13L16 14L15 14L15 15L18 15L18 14L19 14L19 16L21 16L21 13L20 13L20 14L19 14L19 12L21 12L21 10L20 10L20 9L19 9L19 8L18 8L18 9L17 9L17 10L16 10L16 9L15 9L15 8L12 8L12 9L11 9L11 6L12 6L12 7L13 7L13 6L12 6L12 5L13 5L13 3ZM9 6L9 10L8 10L8 9L6 9L6 10L5 10L5 9L4 9L4 10L2 10L2 9L1 9L1 10L2 10L2 11L4 11L4 12L8 12L8 11L9 11L9 10L10 10L10 12L11 12L11 9L10 9L10 6ZM4 10L4 11L5 11L5 10ZM6 10L6 11L8 11L8 10ZM9 13L9 14L10 14L10 13ZM12 14L12 15L14 15L14 14ZM17 16L17 17L18 17L18 16ZM10 17L10 18L11 18L11 17ZM12 17L12 19L14 19L14 18L15 18L15 17ZM9 19L9 20L10 20L10 19ZM0 0L0 7L7 7L7 0ZM1 1L1 6L6 6L6 1ZM2 2L2 5L5 5L5 2ZM14 0L14 7L21 7L21 0ZM15 1L15 6L20 6L20 1ZM16 2L16 5L19 5L19 2ZM0 14L0 21L7 21L7 14ZM1 15L1 20L6 20L6 15ZM2 16L2 19L5 19L5 16Z\" fill=\"#000000\"/></g></g></svg>\n"
```

#### User

| 名稱           | 類型   | 說明                                     | 範例      |
| :------------- | :----- | :--------------------------------------- | :-------- |
| id             | int    | 使用者 ID                                | 6         |
| name           | string | 使用者名字                               | "李大華"  |
| open_id        | string | 使用者 open id                           | "abc123"  |
| avatar_file_id | int    | 大頭照檔案 ID                            | 1         |
| user_type      | string | 使用者類型: 老師(teacher), 學生(student) | "student" |
| username       | string | 使用者登入帳號                           | "stu123"  |

#### Course Stu

| 名稱           | 類型   | 說明                               | 範例                 |
| :------------- | :----- | :--------------------------------- | :------------------- |
| id             | int    | 課堂學生 ID                        | 6                    |
| course_id      | int    | 課堂 ID                            | 6                    |
| user_id        | int    | 使用者 ID 如果訪客學生的話是 0     | 6                    |
| nickname       | string | 暱稱                               | "李大華"             |
| is_visitor     | int    | 是否為訪客學生 是的話是 1 否則為 0 | 1                    |
| score          | int    | 榮譽榜目前的分數                   | 15                   |
| avatar_file_id | int    | 大頭貼檔案 ID                      | 1                    |
| is_online      | int    | 是否在線上                         | 1                    |
| comment        | string | 榮譽榜老師給的評語                 | "非常好"             |
| avatar_file    | json   | 大頭貼檔案內容                     | 參考下方 avatar_file |

#### avatar_file

| 名稱          | 類型   | 說明                                   | 範例                                           |
| :------------ | :----- | :------------------------------------- | :--------------------------------------------- |
| id            | int    | 檔案 ID                                | 6                                              |
| uploader_id   | int    | 上傳者使用者 ID,訪客學生上傳的話會是 0 | 6                                              |
| uploader_type | string | 上傳者類型(student/teacher)            | "student"                                      |
| file_type     | string | 檔案類型                               | "image"                                        |
| course_id     | int    | 上傳者在哪個課堂上傳                   | 1                                              |
| drive_id      | string | 大頭貼檔案位置                         | "GOMQXKw0NRF5CAq3HBOk7fx1cntuk1sxrirZDoCV.png" |

####

### 0. 測試

- [test(GET)-API 測試](#testget-測試) (完成)
- [test(POST)-測試](#testpost-測試) (完成)

### 帳號相關

- [login(POST)-登入](#loginpost-登入) (完成)
- [login_open_id(POST)-OpenID 登入](#loginopenidpost-OpenID登入)
- [logout(POST)-登出](#logoutpost-登出) (完成)

- [users/create(POST)-建立個人資料](#userscreatepost-建立個人資料) (完成)
- [users/{id}(GET)-取得個人資料](#usersidget-取得個人資料) (完成)
- [users/{id}(PUT)-更新個人資料](#usersidput-更新個人資料) (完成)

### 班級/課程相關

- [teachers/{id}/class_subjects(GET)-取得老師所有班級課程](#teachersidclass_subjectsget-取得老師所有班級課程) (完成)

### 課堂相關

- [courses/create(POST)-建立課堂](#coursescreatepost-建立課堂) (完成)
- [courses/{id}(GET)-取得課堂資料](#coursesidget-取得課堂資料) (完成)

- [courses/{id}/online_course_stus(GET)-取得課堂在線所有學生](#coursesidonline_course_stusget-取得課堂在線所有學生) (完成)
- [courses/{id}/last_course_stus(GET)-取得上次課堂學生資料](#coursesidlast_course_stusget-取得上次課堂學生資料) (完成)

- [courses/{id}/actions/open(POST)-開始上課](#coursesidactionsopenpost-開始上課) (完成)
- [courses/{id}/top10(GET)-取得課堂榮譽榜](#coursesidtop10get-取得課堂榮譽榜) (完成)
- [courses/{id}/clean_scores(POST)-清除課堂分數](#coursesidclean_scorespost-清除課堂分數) (完成)

### 老師相關

- [teacher_comments(GET)-取得所有評語](#teacher_commentsget-取得所有評語) (完成)
- [teacher_comments/create(POST)-建立評語](#teacher_commentscreatepost-建立評語) (完成)
- [course_stus/{id}/actions/comment(PUT)-更新學生評語](#course_stusidactionscommentput-更新學生評語) (完成)

### 課堂學生相關

- [course_stus/create(POST)-建立課堂學生](#course_stuscreatepost-建立課堂學生) (完成)
- [course_stus/update(POST)-更新課堂學生](#course_stusupdatepost-更新課堂學生) (完成)
- [course_stus/get_avatars(POST)-取得課堂學生大頭貼](#course_stusget_avatarspost-取得課堂學生大頭貼) (完成)
- [course_score_logs/create(POST)-幫課堂學生分組加減分](#course_score_logscreatepost-幫課堂學生分組加減分) (未完成分組)

### 課堂串流相關
- [MQTT]
- [課堂串流-MQTT](#課堂串流-MQTT) (完成)
- [API]
- [course_streams/create(POST)-建立課堂串流](#course_streamscreatepost-建立課堂串流) (完成)
- [course_streams/{id}(PUT)-更新課堂串流](#course_streamsidput-更新課堂串流) (完成)
- [course_streams/{id}?token={token}&force_get={force_get}(GET)-取得課堂串流資料](#course_streamsid?token=token&force_get=force_getget-取得課堂串流資料) (完成)

### 快問快答相關
- [MQTT]
- [課堂快問快答-MQTT/取得學生個人化狀態說明](#課堂快問快答-mqtt取得學生個人化狀態說明) (完成)
- [API]
- [course_quizzes/create(POST)-建立課堂快問快答](#course_quizzescreatepost-建立課堂快問快答) (完成)
- [course_quizzes/{id}(POST)-更新課堂快問快答](#course_quizzesidPOST-更新課堂快問快答) (完成)
- [course_quizzes/{id}?token={token}&force_get={force_get}(GET)-取得課堂快問快答資料](#course_quizzesidtokentokenforce_getforce_getget-取得課堂快問快答資料) (完成)
- [course_quizzes/{id}/actions/answer(POST)-學生回答快問快答](#course_quizzesidactionsanswerpost-學生回答快問快答) (完成)
- [course_quizzes/{id}/actions/get_answer?course_stu_id={course_stu_id}(GET)-老師取得學生快問快答答案](#course_quizzesidactionsget_answercourse_stu_idcourse_stu_idget-老師取得學生快問快答答案)
- [course_quizzes/{id}/actions/correct(POST)-老師批閱學生快問快答答案](#course_quizzesidactionscorrectpost-老師批閱學生快問快答答案)
- [course_quizzes/{id}/actions/get_correct?token={token}(GET)-學生取得老師快問快答批閱結果](#course_quizzesidactionsget_correcttokentokenget-學生取得老師快問快答批閱結果)
- [course_quizzes/{id}/actions/get_stu_status(GET)-取得學生個人課堂快問快答狀態](#course_quizzesidactionsget_stu_statusget-取得學生個人課堂快問快答狀態) (完成)

### 派送相關

- [course_deliveries/create(POST)-建立課堂派送](#course_deliveriescreatepost-建立課堂派送) (完成)
- [course_deliveries/{id}?token={token}&force_get={force_get}(GET)-取得課堂派送](#course_deliveriesidtokentokenforce_getforce_getget-取得課堂派送) (完成)

### 分組相關
- [MQTT]
- [課堂分組-MQTT](#課堂分組-MQTT) (完成)
- [API]
- [course_teams/create(POST)-建立課堂分組](#course_teamscreatepost-建立課堂分組) (完成)
- [course_teams/{id}(PUT)-更新課堂分組](#course_teamsidput-更新課堂分組) (完成)
- [course_teams/{id}(DELETE)-刪除課堂分組](#course_teamsiddelete-刪除課堂分組) (完成)
- [courses/{id}/course_teams/random_create(POST)-建立隨機課堂分組](#coursesidcourse_teamsrandom_createpost-建立隨機課堂分組) (完成)
- [courses/{id}/course_teams(GET)-取得所有課堂分組](#coursesidcourse_teamsget-取得所有課堂分組) (完成)
- [course_teams/my(GET)-學生取得自己課堂分組](#course_teamsmyget-學生取得自己課堂分組) (完成)

### 抽籤相關

- [course_draw_lots/create(POST)-建立課堂抽籤](#course_draw_lotscreatepost-建立課堂抽籤) (完成)
- [course_draw_lots/{id}(GET)-取得課堂抽籤結果](#course_draw_lotsidget-取得課堂抽籤結果) (完成)
- [courses/{id}/course_draw_lots(GET)-取得課堂所有抽籤結果](#coursesidcourse_draw_lotsget-取得課堂所有抽籤結果) (完成)

### 任務相關
- [MQTT]
- [課堂任務-MQTT/取得學生個人化狀態說明](#課堂任務-mqtt取得學生個人化狀態說明) (完成)
- [API]
- [course_tasks/create(POST)-建立課堂任務](#course_taskscreatepost-建立課堂任務) (完成)
- [course_tasks/{id}(GET)-取得課堂任務](#course_tasksidget-取得課堂任務) (完成)
- [course_tasks/{id}/actions/answer(POST)-學生回答課堂任務](#course_tasksidactionsanswerpost-學生回答課堂任務) (完成)
- [course_tasks/{id}/actions/get_answer?course_stu_id={course_stu_id}(GET)-老師取得學生任務答案](#course_tasksidactionsget_answercourse_stu_idcourse_stu_idget-老師取得學生任務答案)
- [course_tasks/{id}/actions/correct(POST)-老師批閱學生任務答案](#course_tasksidactionscorrectpost-老師批閱學生任務答案)
- [course_tasks/{id}/actions/get_correct?token={token}(GET)-學生取得老師任務批閱結果](#course_tasksidactionsget_correcttokentokenget-學生取得老師任務批閱結果)
- [course_tasks/{id}/actions/close(POST)-老師結束任務](#course_tasksidactionsclosepost-老師結束任務)
- [course_tasks/{id}/actions/get_stu_status(GET)-取得學生個人課堂任務狀態](#course_tasksidactionsget_stu_statusget-取得學生個人課堂任務狀態) (完成)

### 搶答相關
- [MQTT]
- [課堂搶答-MQTT/取得學生個人化狀態說明](#課堂搶答-mqtt取得學生個人化狀態說明) (完成)
- [API]
- [course_qas/create(POST)-建立課堂搶答](#course_qascreatepost-建立課堂搶答) (完成)
- [course_qas/{id}(GET)-取得課堂搶答](#course_qasidget-取得課堂搶答) (完成)
- [course_qas/{id}/actions/run(POST)-開始課堂搶答](#course_qasidactionsrunpost-開始課堂搶答) (完成)
- [course_qas/{id}/actions/stop(POST)-停止課堂搶答](#course_qasidactionsstoppost-停止課堂搶答) (完成)
- [course_qas/{id}/actions/answer(POST)-學生回答課堂搶答](#course_qasidactionsanswerpost-學生回答課堂搶答) (完成)
- [course_qas/{id}/actions/publish_answer(POST)-老師公布競賽搶答答案](#course_qasidactionspublish_answerpost-老師公布競賽搶答答案) (完成)
- [course_qas/{id}/actions/get_result(GET)-取得目前競賽搶答狀況](#course_qasidactionsget_resultget-取得目前競賽搶答狀況) (完成)
- [course_qas/{id}/actions/get_stu_status(GET)-取得學生個人課堂搶答狀態](#course_qasidactionsget_stu_statusget-取得學生個人課堂搶答狀態) (完成)

### 評量相關
- [MQTT]
- [課堂評量-MQTT/取得學生個人化狀態說明](#課堂評量-mqtt取得學生個人化狀態說明) (完成)
- [API]
- [course_assessments/create(POST)-建立課堂評量](#course_assessmentscreatepost-建立課堂評量) (完成)
- [pages/create(POST)-建立課堂評量頁面](#pagescreatepost-建立課堂評量頁面) (完成)
- [pages/{id}(PUT)-更新課堂評量頁面](#pagesidput-更新課堂評量頁面) (完成)
- [pages/{id}(DELETE)-刪除課堂評量頁面](#pagesiddelete-刪除課堂評量頁面) (完成)
- [course_assessments/{id}/actions/run(POST)-開始課堂評量](#course_assessmentsidactionsrunpost-開始課堂評量) (完成)
- [course_assessments/{id}(GET)-取得課堂評量](#course_assessmentsidget-取得課堂評量) (完成)
- [course_assessments/{id}/actions/stop(POST)-停止課堂評量](#course_assessmentsidactionsstoppost-停止課堂評量) (完成)
- [course_assessments/{id}/actions/restart(POST)-重新作答課堂評量](#course_assessmentsidactionsrestartpost-重新作答課堂評量) (完成)
- [course_assessments/{id}/actions/collect(POST)-收卷課堂評量](#course_assessmentsidactionscollectpost-收卷課堂評量) (完成)
- [course_assessments/{id}/actions/correct(POST)-檢討課堂評量](#course_assessmentsidactionscorrectpost-檢討課堂評量) (完成)
- [course_assessments/{id}/actions/publish_answer(POST)-老師公布課堂評量答案](#course_assessmentsidactionspublish_answerpost-老師公布課堂評量答案) (完成)
- [course_assessments/{id}/actions/correct_hand_essay(POST)-老師批閱課堂評量手寫題&文字題](#course_assessmentsidactionscorrect_hand_essaypost-老師批閱課堂評量手寫題文字題) (完成)
- [course_assessments/{id}/actions/answer(POST)-學生回答課堂評量](#course_assessmentsidactionsanswerpost-學生回答課堂評量) (完成)
- [course_assessments/{id}/actions/get_answering_status(GET)-取得課堂評量即時答題狀態](#course_assessmentsidactionsget_answering_statusget-取得課堂評量即時答題狀態) (完成)
- [course_assessments/{id}/actions/get_statistics(GET)-取得課堂評量答題統計](#course_assessmentsidactionsget_statisticsget-取得課堂評量答題統計) (完成)
- [course_assessments/{id}/actions/get_result(GET)-取得學生個人課堂評量結果](#course_assessmentsidactionsget_resultget-取得學生個人課堂評量結果) #待確認 PDF 來源
- [course_assessments/{id}/actions/get_stu_status(GET)-取得學生個人課堂評量狀態](#course_assessmentsidactionsget_stu_statusget-取得學生個人課堂評量狀態) (完成)

- [course_assessments/{id}/actions/export(POST)-匯出課堂評量](#course_assessmentsidactionsexportpost-匯出課堂評量) (完成)
- [course_assessments/{id}/actions/import(POST)-匯入課堂評量](#course_assessmentsidactionsimportpost-匯入課堂評量) (完成)
- [course_assessments/{id}/actions/remove(POST)-移除題庫課堂評量](#course_assessmentsidactionsremovepost-移除題庫課堂評量) (完成)
- [course_assessments/show_tpps(GET)-取得題庫課堂評量](#course_assessmentsshow_tppspost-取得題庫課堂評量) (完成)

### test(GET)-測試

#### Request

- Method: **GET**
- URL: `test`
- Headers:
- Path-params:

無須輸入參數

#### Response

-成功

- Body:

```json
{
  "result": true,
  "msg": ["The API was successfully accessed."],
  "data": []
}
```

### test(POST)-測試

#### Request

- Method: **POST**
- URL: `test`
- Headers: Content-Type:multipart/form-data
- Path-params:

#### Response

-成功

- Body:

```json
{
  "result": true,
  "data": {
    "class_name": "一年三班",
    "subject": "英文"
  },
  "msg": ["The API was successfully accessed.Data Just show what you post"]
}
```

### login(POST)-登入

#### Request

- Method: **POST**
- URL: `login`
- Headers: Content-Type:multipart/form-data
- Path-params:

| 名稱     | 類型   | 說明 | 範例    | 是否必須 |
| :------- | :----- | :--- | :------ | :------- |
| username | String | 帳號 | test001 | O        |
| password | String | 密碼 | 123456  | O        |

#### Response

-成功

- Body:

```json
{
  "result": true,
  "msg": ["Success"],
  "data": {
    "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJodHRwOi8vMTI3LjAuMC4xOjgwMDAvbG9naW4iLCJpYXQiOjE3MDM4NTA5NzYsImV4cCI6MTcwMzg1NDU3NiwibmJmIjoxNzAzODUwOTc2LCJqdGkiOiJpVWN2Zk00dnNORTlMZlNiIiwic3ViIjoiMiIsInBydiI6IjIzYmQ1Yzg5NDlmNjAwYWRiMzllNzAxYzQwMDg3MmRiN2E1OTc2ZjcifQ.t_O6ulJ4A9RSh35UTFYdlni4bKrno2u2AWjA1dMnMpY",
    "token_type": "bearer",
    "expires_in": 3600,
    "id": 2
  }
}
```

-失敗

### 帳號或密碼錯誤

- Body:

```json
{
  "result": false,
  "msg": ["Username or password error."]
}
```

### 帶同樣的 token 來 login

- Body:

```json
{
  "result": false,
  "msg": ["User is already logged in."]
}
```

### logout(POST)-登出

#### Request

- Method: **POST**
- URL: `logout`
- Headers: Content-Type:multipart/form-data
- Path-params:

| 名稱         | 類型 | 說明 | 範例 | 是否必須 |
| :----------- | :--- | :--- | :--- | :------- |
| Bearer Token |      |      |      | O        |

#### Response

-成功

- Body:

```json
{
  "result": true,
  "msg": ["Success"],
  "data": []
}
```

-失敗

### 使用者未登入

- Status: 401 Unauthorized
- Body:

```json
{
  "result": false,
  "msg": ["The user is not logged in."]
}
```

### users/create(POST)-建立個人資料

#### Request

- Method: **POST**
- URL: `users/create`
- Headers: Content-Type:multipart/form-data
- Path-params:

| 名稱         | 類型   | 說明                       | 範例         | 是否必須 |
| :----------- | :----- | :------------------------- | :----------- | :------- |
| username     | string | 帳號                       | test123      | O        |
| name         | string | 名字                       | 王小明       | O        |
| password     | string | 密碼                       | qq123        | O        |
| user_type    | string | 使用者類型:student,teacher | student      | O        |
| open_id      | email  | 教育部 open id             | test@abc.com | X        |
| Bearer Token |        |                            |              | O        |

#### Response

-成功

- Body:

```json
{
  "result": true,
  "msg": ["Success"],
  "data": {
    "id": 3
  }
}
```

-失敗

### 參數錯誤

- Body:

```json
{
  "result": false,
  "msg": [
    "username:The username field is required.",
    "name:The name field is required.",
    "password:The password field is required.",
    "user_type:The user type field is required.",
    "open_id:The open id must be a valid email address."
  ]
}
```

### users/{id}(GET)-取得個人資料

#### Request

- Method: **GET**
- URL: `users/{id}`
- Headers:
- Path-params:

| 名稱         | 類型 | 說明                                                                      | 範例 | 是否必須 |
| :----------- | :--- | :------------------------------------------------------------------------ | :--- | :------- |
| id           | int  | 使用者 ID, 若沒有給就是取得登入者本人資料(但目前也只能取得個人自己的資料) | 1    | X        |
| Bearer Token |      |                                                                           |      | O        |

#### Response

-成功

- Body:

老師

```json
{
  "result": true,
  "msg": ["Success"],
  "data": [
    {
      "id": 2,
      "name": "李大華",
      "created_at": "2023-12-28T02:36:26.000000Z",
      "updated_at": "2023-12-28T02:36:26.000000Z",
      "open_id": null,
      "avatar_file_id": 1,
      "user_type": "teacher",
      "username": "teacher"
    }
  ]
}
```

學生

```json
{
  "result": true,
  "msg": ["Success"],
  "data": [
    {
      "id": 3,
      "name": "王晶晶",
      "created_at": "2023-12-29T12:23:00.000000Z",
      "updated_at": "2023-12-29T12:23:00.000000Z",
      "open_id": null,
      "avatar_file_id": 2,
      "user_type": "student",
      "username": "stu01"
    }
  ]
}
```

-失敗

#### 沒有權限

- Body:

```json
{
  "result": false,
  "msg": ["You do not have permission to access this resource."]
}
```

### users/{id}(PUT)-更新個人資料

#### Request

- Method: **PUT**
- URL: `users/{id}`
- Headers: Content-Type:multipart/form-data
- Path-params:

| 名稱         | 類型   | 說明 | 範例   | 是否必須 |
| :----------- | :----- | :--- | :----- | :------- |
| name         | string | 名字 | 王小明 | O        |
| Bearer Token |        |      |        | O        |

#### Response

-成功

- Body:

```json
{
  "result": true,
  "msg": ["Success"],
  "data": []
}
```

-失敗

#### 沒有權限 (非本人)

- Body:

```json
{
  "result": false,
  "msg": ["You are not allowed to do this action."]
}
```

### 帳號重複

- Body:

```json
{
  "result": false,
  "msg": ["username:The username has already been taken."]
}
```

### teachers/{id}/class_subjects(GET)-取得老師所有班級課程

#### Request

- Method: **GET**
- URL: `teachers/{id}/class_subjects`
- Headers:
- Path-params:

| 名稱         | 類型 | 說明          | 範例 | 是否必須 |
| :----------- | :--- | :------------ | :--- | :------- |
| id           | int  | 老師使用者 ID | 1    | O        |
| Bearer Token |      |               |      | O        |

#### Response

-成功

- Body:

```json
{
  "result": true,
  "msg": ["Success"],
  "data": {
    "class_name": ["一年一班", "一年三班"],
    "subjects": ["數學", "英文"]
  }
}
```

-失敗

### 不是該老師

- Body:

```json
{
  "result": false,
  "msg": ["You do not have permission to access this resource."]
}
```

### courses/create(POST)-建立課堂

#### Request

- Method: **POST**
- URL: `courses/create`
- Headers: Content-Type:multipart/form-data
- Path-params:

| 名稱         | 類型   | 說明 | 範例     | 是否必須 |
| :----------- | :----- | :--- | :------- | :------- |
| class_name   | string | 班級 | 一年三班 | O        |
| subject      | string | 科目 | 英文     | O        |
| Bearer Token |        |      |          | O        |

#### Response

-成功

- Body:

```json
{
  "result": true,
  "msg": ["Success"],
  "data": {
    "class_name": "一年三班",
    "subject": "英文",
    "user_id": 2,
    "code": "zIKvUMuB7T",
    "is_open": false,
    "qrcode_svg": "<?xml version=\"1.0\" encoding=\"UTF-8\"?>\n<svg xmlns=\"http://www.w3.org/2000/svg\" version=\"1.1\" width=\"100\" height=\"100\" viewBox=\"0 0 100 100\"><rect x=\"0\" y=\"0\" width=\"100\" height=\"100\" fill=\"#ffffff\"/><g transform=\"scale(4.762)\"><g transform=\"translate(0,0)\"><path fill-rule=\"evenodd\" d=\"M10 0L10 1L11 1L11 0ZM12 0L12 2L13 2L13 0ZM8 2L8 3L9 3L9 2ZM10 2L10 3L11 3L11 2ZM12 3L12 4L11 4L11 5L10 5L10 4L9 4L9 6L8 6L8 8L4 8L4 9L3 9L3 8L0 8L0 11L2 11L2 12L0 12L0 13L2 13L2 12L3 12L3 13L8 13L8 17L9 17L9 18L8 18L8 21L10 21L10 20L11 20L11 21L12 21L12 20L14 20L14 21L21 21L21 20L20 20L20 19L21 19L21 18L20 18L20 17L19 17L19 18L20 18L20 19L19 19L19 20L14 20L14 19L17 19L17 18L16 18L16 16L12 16L12 17L11 17L11 16L10 16L10 14L11 14L11 13L12 13L12 12L13 12L13 13L14 13L14 11L12 11L12 9L13 9L13 10L14 10L14 9L15 9L15 11L19 11L19 12L18 12L18 13L17 13L17 12L15 12L15 13L16 13L16 14L15 14L15 15L18 15L18 14L19 14L19 16L21 16L21 13L20 13L20 14L19 14L19 12L21 12L21 10L20 10L20 9L19 9L19 8L18 8L18 9L17 9L17 10L16 10L16 9L15 9L15 8L12 8L12 9L11 9L11 6L12 6L12 7L13 7L13 6L12 6L12 5L13 5L13 3ZM9 6L9 10L8 10L8 9L6 9L6 10L5 10L5 9L4 9L4 10L2 10L2 9L1 9L1 10L2 10L2 11L4 11L4 12L8 12L8 11L9 11L9 10L10 10L10 12L11 12L11 9L10 9L10 6ZM4 10L4 11L5 11L5 10ZM6 10L6 11L8 11L8 10ZM9 13L9 14L10 14L10 13ZM12 14L12 15L14 15L14 14ZM17 16L17 17L18 17L18 16ZM10 17L10 18L11 18L11 17ZM12 17L12 19L14 19L14 18L15 18L15 17ZM9 19L9 20L10 20L10 19ZM0 0L0 7L7 7L7 0ZM1 1L1 6L6 6L6 1ZM2 2L2 5L5 5L5 2ZM14 0L14 7L21 7L21 0ZM15 1L15 6L20 6L20 1ZM16 2L16 5L19 5L19 2ZM0 14L0 21L7 21L7 14ZM1 15L1 20L6 20L6 15ZM2 16L2 19L5 19L5 16Z\" fill=\"#000000\"/></g></g></svg>\n",
    "updated_at": "2024-01-15 10:29:20",
    "created_at": "2024-01-15 10:29:20",
    "id": 8
  }
}
```

-失敗

#### 沒有權限(不是老師)

- Status: 403 Forbidden
- Body:

```json
{
  "result": false,
  "msg": ["You do not have permission to access this resource."]
}
```

### courses/{id}(GET)-取得課堂資料

#### Request

- Method: **GET**
- URL: `courses/{id}`
- Headers:
- Path-params:

| 名稱 | 類型 | 說明                   | 範例 | 是否必須 |
| :--- | :--- | :--------------------- | :--- | :------- |
| id   | int  | 課堂 ID/或課堂碼(code) | 1    | O        |

#### Response

-成功

- Body:

```json
{
  "result": true,
  "msg": ["Success"],
  "data": [
    {
      "id": 6,
      "user_id": 2,
      "class_name": "一年三班",
      "subject": "英文",
      "code": "BpQYoYzMZm",
      "is_open": 0,
      "status": null, //broadcast
      "status_id": 1, //broadcast
      "created_at": "2023-12-29 20:48:18",
      "updated_at": "2023-12-29 20:48:18",
      "deleted_at": null,
      "user": {
        "id": 2,
        "name": "李大華",
        "created_at": "2023-12-28T02:36:26.000000Z",
        "updated_at": "2023-12-28T02:36:26.000000Z",
        "open_id": null,
        "avatar_file_id": null,
        "user_type": "teacher",
        "username": "teacher"
      }
    }
  ]
}
```

-失敗

### 課堂不存在

- Status: 404 Not Found

### courses/{id}/online_course_stus(GET)-取得課堂在線所有學生

#### Request

- Method: **GET**
- URL: `courses/{id}/online_course_stus`
- Headers:
- Path-params:

| 名稱 | 類型 | 說明    | 範例 | 是否必須 |
| :--- | :--- | :------ | :--- | :------- |
| id   | int  | 課堂 ID | 1    | O        |

#### Response

-成功

- Body:

```json
{
  "result": true,
  "msg": ["Success"],
  "data": [
    {
      "id": 4,
      "course_id": 1,
      "user_id": 0,
      "nickname": "小火",
      "is_visitor": 1,
      "score": 0,
      "avatar_file_id": 1,
      "is_online": 1,
      "created_at": "2023-12-30 11:39:56",
      "updated_at": "2023-12-30 11:39:56",
      "deleted_at": null
    },
    {
      "id": 5,
      "course_id": 1,
      "user_id": 0,
      "nickname": "小土",
      "is_visitor": 1,
      "score": 0,
      "avatar_file_id": 1,
      "is_online": 1,
      "created_at": "2023-12-30 13:06:05",
      "updated_at": "2023-12-30 13:06:05",
      "deleted_at": null
    }
  ]
}
```

-失敗

### 課堂不存在

- Status: 404 Not Found

### courses/{id}/last_course_stus(GET)-取得上次課堂學生資料

#### Request

- Method: **GET**
- URL: `courses/{id}/last_course_stus`
- Headers:
- Path-params:

| 名稱 | 類型 | 說明    | 範例 | 是否必須 |
| :--- | :--- | :------ | :--- | :------- |
| id   | int  | 課堂 ID | 1    | O        |

#### Response

-成功

- Body:

```json
{
  "result": true,
  "msg": ["Success"],
  "data": [
    {
      "id": 1,
      "course_id": 1,
      "user_id": 0,
      "nickname": "小金",
      "is_visitor": 1,
      "score": 0,
      "avatar_file_id": 1,
      "is_online": 0,
      "created_at": "2023-12-29 09:24:06",
      "updated_at": "2023-12-29 09:24:06",
      "deleted_at": null,
      "avatar_file": {
        "id": 1,
        "uploader_id": 0,
        "uploader_type": "student",
        "file_type": "image",
        "course_id": 1,
        "drive_id": "GOMQXKw0NRF5CAq3HBOk7fx1cntuk1sxrirZDoCV.png",
        "created_at": "2023-12-30 11:32:58",
        "updated_at": "2023-12-30 11:32:58",
        "deleted_at": null
      }
    },
    {
      "id": 4,
      "course_id": 1,
      "user_id": 0,
      "nickname": "小火",
      "is_visitor": 1,
      "score": 0,
      "avatar_file_id": 1,
      "is_online": 1,
      "created_at": "2023-12-30 11:39:56",
      "updated_at": "2023-12-30 11:39:56",
      "deleted_at": null,
      "avatar_file": {
        "id": 1,
        "uploader_id": 0,
        "uploader_type": "student",
        "file_type": "image",
        "course_id": 1,
        "drive_id": "GOMQXKw0NRF5CAq3HBOk7fx1cntuk1sxrirZDoCV.png",
        "created_at": "2023-12-30 11:32:58",
        "updated_at": "2023-12-30 11:32:58",
        "deleted_at": null
      }
    },
    {
      "id": 5,
      "course_id": 1,
      "user_id": 0,
      "nickname": "小土",
      "is_visitor": 1,
      "score": 0,
      "avatar_file_id": 1,
      "is_online": 1,
      "created_at": "2023-12-30 13:06:05",
      "updated_at": "2023-12-30 13:06:05",
      "deleted_at": null,
      "avatar_file": {
        "id": 1,
        "uploader_id": 0,
        "uploader_type": "student",
        "file_type": "image",
        "course_id": 1,
        "drive_id": "GOMQXKw0NRF5CAq3HBOk7fx1cntuk1sxrirZDoCV.png",
        "created_at": "2023-12-30 11:32:58",
        "updated_at": "2023-12-30 11:32:58",
        "deleted_at": null
      }
    }
  ]
}
```

-失敗

### 課堂不存在

- Status: 404 Not Found

### courses/{id}/actions/open(POST)-開始上課

#### Request

- Method: **POST**
- URL: `courses/{id}/actions/open`
- Headers: Content-Type:multipart/form-data
- Path-params:

| 名稱         | 類型 | 說明    | 範例  | 是否必須 |
| :----------- | :--- | :------ | :---- | :------- |
| id           | int  | 課堂 ID | 12345 | O        |
| Bearer Token |      |         |       | O        |

#### Response

-成功

- Body:

```json
{
  "result": true,
  "msg": ["Success"],
  "data": {
    "code": "yMdlXBrpo9",
    "qrcode": "<?xml version=\"1.0\" encoding=\"UTF-8\"?>\n<svg xmlns=\"http://www.w3.org/2000/svg\" version=\"1.1\" width=\"100\" height=\"100\" viewBox=\"0 0 100 100\"><rect x=\"0\" y=\"0\" width=\"100\" height=\"100\" fill=\"#ffffff\"/><g transform=\"scale(4.762)\"><g transform=\"translate(0,0)\"><path fill-rule=\"evenodd\" d=\"M8 0L8 1L9 1L9 2L8 2L8 5L11 5L11 4L12 4L12 3L13 3L13 0L12 0L12 3L11 3L11 2L10 2L10 0ZM9 2L9 4L11 4L11 3L10 3L10 2ZM8 6L8 7L9 7L9 8L8 8L8 9L9 9L9 10L6 10L6 9L7 9L7 8L6 8L6 9L4 9L4 8L0 8L0 9L1 9L1 10L0 10L0 11L3 11L3 12L2 12L2 13L8 13L8 14L9 14L9 16L10 16L10 17L8 17L8 21L9 21L9 19L10 19L10 17L12 17L12 16L13 16L13 19L12 19L12 18L11 18L11 21L14 21L14 20L15 20L15 19L14 19L14 18L15 18L15 17L14 17L14 16L13 16L13 15L11 15L11 13L12 13L12 12L13 12L13 9L14 9L14 8L13 8L13 9L12 9L12 12L10 12L10 14L9 14L9 12L8 12L8 11L9 11L9 10L10 10L10 9L11 9L11 6L10 6L10 7L9 7L9 6ZM12 6L12 7L13 7L13 6ZM9 8L9 9L10 9L10 8ZM16 8L16 10L14 10L14 11L16 11L16 10L18 10L18 9L19 9L19 8ZM20 8L20 9L21 9L21 8ZM2 9L2 10L3 10L3 11L4 11L4 9ZM19 10L19 11L21 11L21 10ZM6 11L6 12L7 12L7 11ZM17 11L17 12L18 12L18 11ZM0 12L0 13L1 13L1 12ZM14 12L14 13L13 13L13 14L14 14L14 15L15 15L15 16L17 16L17 17L16 17L16 18L18 18L18 19L19 19L19 18L20 18L20 17L19 17L19 15L17 15L17 13L16 13L16 12ZM20 12L20 13L19 13L19 14L20 14L20 13L21 13L21 12ZM14 13L14 14L15 14L15 13ZM20 15L20 16L21 16L21 15ZM13 19L13 20L14 20L14 19ZM20 19L20 20L21 20L21 19ZM17 20L17 21L18 21L18 20ZM0 0L0 7L7 7L7 0ZM1 1L1 6L6 6L6 1ZM2 2L2 5L5 5L5 2ZM14 0L14 7L21 7L21 0ZM15 1L15 6L20 6L20 1ZM16 2L16 5L19 5L19 2ZM0 14L0 21L7 21L7 14ZM1 15L1 20L6 20L6 15ZM2 16L2 19L5 19L5 16Z\" fill=\"#000000\"/></g></g></svg>\n"
  }
}
```

-失敗

#### 沒有權限(不是該課堂老師)

- Status: 403 Forbidden
- Body:

```json
{
  "result": false,
  "msg": ["You do not have permission to access this resource."]
}
```

### courses/{id}/top10(GET)-取得課堂榮譽榜

#### Request

- Method: **GET**
- URL: `courses/{id}/top10`
- Headers:
- Path-params:

| 名稱         | 類型 | 說明             | 範例 | 是否必須 |
| :----------- | :--- | :--------------- | :--- | :------- |
| id           | int  | 課堂 ID          | 1    | O        |
| Bearer Token |      | 有登入的話必須要 |      | X        |
| token        |      | 訪客學生必須要   |      | X        |

#### Response

-成功 (學生取的話會包含自己的分數)

- Body:

```json (老師)
{
  "result": true,
  "msg": ["Success"],
  "data": {
    "top10": [
      {
        "id": 1,
        "course_id": 1,
        "user_id": 0,
        "nickname": "小金",
        "is_visitor": 1,
        "score": 15,
        "avatar_file_id": 1,
        "is_online": 0,
        "created_at": "2023-12-29 09:24:06",
        "updated_at": "2024-01-19 11:15:51",
        "deleted_at": null,
        "stream_url": null,
        "comment": "",
        "avatar_file": {
          "id": 1,
          "uploader_id": 0,
          "uploader_type": "student",
          "file_type": "image",
          "course_id": 1,
          "drive_id": "GOMQXKw0NRF5CAq3HBOk7fx1cntuk1sxrirZDoCV.png",
          "created_at": "2023-12-30 11:32:58",
          "updated_at": "2023-12-30 11:32:58",
          "deleted_at": null
        }
      },
      {
        "id": 5,
        "course_id": 1,
        "user_id": 0,
        "nickname": "小土",
        "is_visitor": 1,
        "score": 10,
        "avatar_file_id": 1,
        "is_online": 1,
        "created_at": "2023-12-30 13:06:05",
        "updated_at": "2024-01-19 11:17:15",
        "deleted_at": null,
        "stream_url": null,
        "comment": "",
        "avatar_file": {
          "id": 1,
          "uploader_id": 0,
          "uploader_type": "student",
          "file_type": "image",
          "course_id": 1,
          "drive_id": "GOMQXKw0NRF5CAq3HBOk7fx1cntuk1sxrirZDoCV.png",
          "created_at": "2023-12-30 11:32:58",
          "updated_at": "2023-12-30 11:32:58",
          "deleted_at": null
        }
      },
      {
        "id": 4,
        "course_id": 1,
        "user_id": 0,
        "nickname": "小火",
        "is_visitor": 1,
        "score": 5,
        "avatar_file_id": 1,
        "is_online": 1,
        "created_at": "2023-12-30 11:39:56",
        "updated_at": "2023-12-30 11:39:56",
        "deleted_at": null,
        "stream_url": null,
        "comment": "",
        "avatar_file": {
          "id": 1,
          "uploader_id": 0,
          "uploader_type": "student",
          "file_type": "image",
          "course_id": 1,
          "drive_id": "GOMQXKw0NRF5CAq3HBOk7fx1cntuk1sxrirZDoCV.png",
          "created_at": "2023-12-30 11:32:58",
          "updated_at": "2023-12-30 11:32:58",
          "deleted_at": null
        }
      },
      {
        "id": 7,
        "course_id": 1,
        "user_id": 3,
        "nickname": "晶晶",
        "is_visitor": 0,
        "score": 0,
        "avatar_file_id": 0,
        "is_online": 1,
        "created_at": "2024-01-03 17:23:21",
        "updated_at": "2024-01-03 17:23:21",
        "deleted_at": null,
        "stream_url": null,
        "comment": "",
        "avatar_file": null
      },
      {
        "id": 9,
        "course_id": 1,
        "user_id": 0,
        "nickname": "甜甜",
        "is_visitor": 1,
        "score": 0,
        "avatar_file_id": 0,
        "is_online": 1,
        "created_at": "2024-01-04 12:00:57",
        "updated_at": "2024-01-04 12:00:57",
        "deleted_at": null,
        "stream_url": null,
        "comment": "",
        "avatar_file": null
      },
      {
        "id": 10,
        "course_id": 1,
        "user_id": 0,
        "nickname": "心心",
        "is_visitor": 1,
        "score": 0,
        "avatar_file_id": 0,
        "is_online": 1,
        "created_at": "2024-01-13 17:25:22",
        "updated_at": "2024-01-13 17:25:22",
        "deleted_at": null,
        "stream_url": null,
        "comment": "",
        "avatar_file": null
      },
      {
        "id": 11,
        "course_id": 1,
        "user_id": 0,
        "nickname": "心心",
        "is_visitor": 1,
        "score": 0,
        "avatar_file_id": 0,
        "is_online": 1,
        "created_at": "2024-01-14 13:40:45",
        "updated_at": "2024-01-14 13:40:45",
        "deleted_at": null,
        "stream_url": null,
        "comment": "",
        "avatar_file": null
      },
      {
        "id": 12,
        "course_id": 1,
        "user_id": 3,
        "nickname": "小明",
        "is_visitor": 0,
        "score": 0,
        "avatar_file_id": 0,
        "is_online": 1,
        "created_at": "2024-01-14 13:46:10",
        "updated_at": "2024-01-14 13:46:10",
        "deleted_at": null,
        "stream_url": null,
        "comment": "",
        "avatar_file": null
      },
      {
        "id": 13,
        "course_id": 1,
        "user_id": 0,
        "nickname": "心心",
        "is_visitor": 1,
        "score": 0,
        "avatar_file_id": 0,
        "is_online": 1,
        "created_at": "2024-01-14 14:31:34",
        "updated_at": "2024-01-14 14:31:34",
        "deleted_at": null,
        "stream_url": null,
        "comment": "",
        "avatar_file": null
      },
      {
        "id": 15,
        "course_id": 1,
        "user_id": 0,
        "nickname": "心心",
        "is_visitor": 1,
        "score": 0,
        "avatar_file_id": 0,
        "is_online": 1,
        "created_at": "2024-01-16 22:36:33",
        "updated_at": "2024-01-16 22:36:33",
        "deleted_at": null,
        "stream_url": null,
        "comment": "",
        "avatar_file": null
      }
    ]
  }
}
```

```json 學生
{
  "result": true,
  "msg": ["Success"],
  "data": {
    "top10": [
      {
        "id": 1,
        "course_id": 1,
        "user_id": 0,
        "nickname": "小金",
        "is_visitor": 1,
        "score": 15,
        "avatar_file_id": 1,
        "is_online": 0,
        "created_at": "2023-12-29 09:24:06",
        "updated_at": "2024-01-19 11:15:51",
        "deleted_at": null,
        "stream_url": null,
        "comment": "",
        "avatar_file": {
          "id": 1,
          "uploader_id": 0,
          "uploader_type": "student",
          "file_type": "image",
          "course_id": 1,
          "drive_id": "GOMQXKw0NRF5CAq3HBOk7fx1cntuk1sxrirZDoCV.png",
          "created_at": "2023-12-30 11:32:58",
          "updated_at": "2023-12-30 11:32:58",
          "deleted_at": null
        }
      },
      {
        "id": 5,
        "course_id": 1,
        "user_id": 0,
        "nickname": "小土",
        "is_visitor": 1,
        "score": 10,
        "avatar_file_id": 1,
        "is_online": 1,
        "created_at": "2023-12-30 13:06:05",
        "updated_at": "2024-01-19 11:17:15",
        "deleted_at": null,
        "stream_url": null,
        "comment": "",
        "avatar_file": {
          "id": 1,
          "uploader_id": 0,
          "uploader_type": "student",
          "file_type": "image",
          "course_id": 1,
          "drive_id": "GOMQXKw0NRF5CAq3HBOk7fx1cntuk1sxrirZDoCV.png",
          "created_at": "2023-12-30 11:32:58",
          "updated_at": "2023-12-30 11:32:58",
          "deleted_at": null
        }
      },
      {
        "id": 4,
        "course_id": 1,
        "user_id": 0,
        "nickname": "小火",
        "is_visitor": 1,
        "score": 5,
        "avatar_file_id": 1,
        "is_online": 1,
        "created_at": "2023-12-30 11:39:56",
        "updated_at": "2023-12-30 11:39:56",
        "deleted_at": null,
        "stream_url": null,
        "comment": "",
        "avatar_file": {
          "id": 1,
          "uploader_id": 0,
          "uploader_type": "student",
          "file_type": "image",
          "course_id": 1,
          "drive_id": "GOMQXKw0NRF5CAq3HBOk7fx1cntuk1sxrirZDoCV.png",
          "created_at": "2023-12-30 11:32:58",
          "updated_at": "2023-12-30 11:32:58",
          "deleted_at": null
        }
      },
      {
        "id": 7,
        "course_id": 1,
        "user_id": 3,
        "nickname": "晶晶",
        "is_visitor": 0,
        "score": 0,
        "avatar_file_id": 0,
        "is_online": 1,
        "created_at": "2024-01-03 17:23:21",
        "updated_at": "2024-01-03 17:23:21",
        "deleted_at": null,
        "stream_url": null,
        "comment": "",
        "avatar_file": null
      },
      {
        "id": 9,
        "course_id": 1,
        "user_id": 0,
        "nickname": "甜甜",
        "is_visitor": 1,
        "score": 0,
        "avatar_file_id": 0,
        "is_online": 1,
        "created_at": "2024-01-04 12:00:57",
        "updated_at": "2024-01-04 12:00:57",
        "deleted_at": null,
        "stream_url": null,
        "comment": "",
        "avatar_file": null
      },
      {
        "id": 10,
        "course_id": 1,
        "user_id": 0,
        "nickname": "心心",
        "is_visitor": 1,
        "score": 0,
        "avatar_file_id": 0,
        "is_online": 1,
        "created_at": "2024-01-13 17:25:22",
        "updated_at": "2024-01-13 17:25:22",
        "deleted_at": null,
        "stream_url": null,
        "comment": "",
        "avatar_file": null
      },
      {
        "id": 11,
        "course_id": 1,
        "user_id": 0,
        "nickname": "心心",
        "is_visitor": 1,
        "score": 0,
        "avatar_file_id": 0,
        "is_online": 1,
        "created_at": "2024-01-14 13:40:45",
        "updated_at": "2024-01-14 13:40:45",
        "deleted_at": null,
        "stream_url": null,
        "comment": "",
        "avatar_file": null
      },
      {
        "id": 12,
        "course_id": 1,
        "user_id": 3,
        "nickname": "小明",
        "is_visitor": 0,
        "score": 0,
        "avatar_file_id": 0,
        "is_online": 1,
        "created_at": "2024-01-14 13:46:10",
        "updated_at": "2024-01-14 13:46:10",
        "deleted_at": null,
        "stream_url": null,
        "comment": "",
        "avatar_file": null
      },
      {
        "id": 13,
        "course_id": 1,
        "user_id": 0,
        "nickname": "心心",
        "is_visitor": 1,
        "score": 0,
        "avatar_file_id": 0,
        "is_online": 1,
        "created_at": "2024-01-14 14:31:34",
        "updated_at": "2024-01-14 14:31:34",
        "deleted_at": null,
        "stream_url": null,
        "comment": "",
        "avatar_file": null
      },
      {
        "id": 15,
        "course_id": 1,
        "user_id": 0,
        "nickname": "心心",
        "is_visitor": 1,
        "score": 0,
        "avatar_file_id": 0,
        "is_online": 1,
        "created_at": "2024-01-16 22:36:33",
        "updated_at": "2024-01-16 22:36:33",
        "deleted_at": null,
        "stream_url": null,
        "comment": "",
        "avatar_file": null
      }
    ],
    "my_score": {
      "id": 12,
      "course_id": 1,
      "user_id": 3,
      "nickname": "小明",
      "is_visitor": 0,
      "score": 0,
      "avatar_file_id": 0,
      "is_online": 1,
      "created_at": "2024-01-14 13:46:10",
      "updated_at": "2024-01-14 13:46:10",
      "deleted_at": null,
      "stream_url": null,
      "comment": "",
      "rank": 4
    }
  }
}
```

-失敗

### 課堂不存在

- Status: 404 Not Found

### courses/{id}/clean_scores(POST)-清除課堂分數

#### Request

- Method: **POST**
- URL: `courses/{id}/clean_scores`
- Headers: Content-Type:multipart/form-data
- Path-params:

| 名稱         | 類型 | 說明    | 範例  | 是否必須 |
| :----------- | :--- | :------ | :---- | :------- |
| id           | int  | 課堂 ID | 12345 | O        |
| Bearer Token |      |         |       | O        |

#### Response

-成功

- Body:

```json
{
  "result": true,
  "msg": ["Success"],
  "data": []
}
```

-失敗

#### 沒有權限(不是該課堂老師)

- Status: 403 Forbidden
- Body:

```json
{
  "result": false,
  "msg": ["You do not have permission to access this resource."]
}
```

### teacher_comments(GET)-取得所有評語

#### Request

- Method: **GET**
- URL: `teacher_comments`
- Headers:
- Path-params:

| 名稱         | 類型 | 說明         | 範例 | 是否必須 |
| :----------- | :--- | :----------- | :--- | :------- |
| Bearer Token |      | 只有老師可用 |      | O        |

#### Response

-成功

- Body:

```json
{
  "result": true,
  "msg": ["Success"],
  "data": [
    {
      "id": 1,
      "comment": "表現優良",
      "user_id": 2,
      "created_at": "2024-01-20 11:16:24",
      "updated_at": "2024-01-20 11:16:24",
      "deleted_at": null
    },
    {
      "id": 2,
      "comment": "表現優異",
      "user_id": 2,
      "created_at": "2024-01-20 11:22:23",
      "updated_at": "2024-01-20 11:22:23",
      "deleted_at": null
    }
  ]
}
```

-失敗

#### 沒有權限(不是老師)

- Status: 403 Forbidden
- Body:

```json
{
  "result": false,
  "msg": ["You do not have permission to access this resource."]
}
```

### teacher_comments/create(POST)-建立評語

#### Request

- Method: **POST**
- URL: `teacher_comments/create`
- Headers: Content-Type:multipart/form-data
- Path-params:

| 名稱         | 類型   | 說明         | 範例     | 是否必須 |
| :----------- | :----- | :----------- | :------- | :------- |
| comment      | string | 評語         | 表現優良 | O        |
| Bearer Token |        | 只有老師可用 |          | O        |

#### Response

-成功

- Body:

```json
{
  "result": true,
  "msg": ["Success"],
  "data": {
    "comment": "表現優異",
    "user_id": 2,
    "updated_at": "2024-01-20 11:22:23",
    "created_at": "2024-01-20 11:22:23",
    "id": 2
  }
}
```

-失敗

#### 沒有權限(不是老師)

- Status: 403 Forbidden
- Body:

```json
{
  "result": false,
  "msg": ["You do not have permission to access this resource."]
}
```

### course_stus/{id}/actions/comment(PUT)-更新學生評語

#### Request

- Method: **PUT**
- URL: `course_stus/{id}/actions/comment`
- Headers: Content-Type:multipart/form-data
- Path-params:

| 名稱         | 類型   | 說明         | 範例     | 是否必須 |
| :----------- | :----- | :----------- | :------- | :------- |
| id           | int    | 課堂學生 ID  | 1        | O        |
| comment      | string | 評語         | 表現優良 | O        |
| Bearer Token |        | 只有老師可用 |          | O        |

#### Response

-成功

- Body:

```json
{
  "result": true,
  "msg": ["Success"],
  "data": {
    "id": 1
  }
}
```

-失敗

#### 沒有權限(不是老師)

- Status: 403 Forbidden
- Body:

```json
{
  "result": false,
  "msg": ["You do not have permission to access this resource."]
}
```

### course_stus/create(POST)-建立課堂學生

#### Request

- Method: **POST**
- URL: `course_stus/create`
- Headers: Content-Type:multipart/form-data
- Path-params:

| 名稱         | 類型    | 說明                                  | 範例       | 是否必須      |
| :----------- | :------ | :------------------------------------ | :--------- | :------------ |
| nickname     | string  | 姓名                                  | 王小明     | X(匿名才必須) |
| is_visitor   | boolean | 是否為訪客，若不是需要傳 bearer token | true       | O             |
| course_id    | int     | 課程 ID (和課程碼擇一傳送)            | 1          | x             |
| code         | string  | 課程碼 (和課程 ID 擇一傳送)           | yMdlXBrpo9 | x             |
| avatar_file  | file    | 照片檔案，若未傳送會用預設照片        |            | X             |
| Bearer Token |         | 有登入學生需傳否則視為訪客            |            | X             |

#### Response

-成功

訪客的話會有 token, 之後發送 request 需要發送 token

- Body:

```json 不是訪客
{
  "result": true,
  "msg": ["Success"],
  "data": {
    "id": 6
  }
}
```

```json 訪客
{
  "result": true,
  "msg": ["Success"],
  "data": {
    "id": 10,
    "token": "10-d401f35993b3f038d24c552b9b3c3a53"
  }
}
```

-失敗

#### 課堂不存在

- Body:

```json
{
  "result": false,
  "msg": ["The course is not started."]
}
```

#### 課堂未開課

- Body:

```json
{
  "result": false,
  "msg": ["The course is not started."]
}
```

#### 選擇不是訪客但未登入

- Body:

```json
{
  "result": false,
  "msg": ["Please login or select visitor."]
}
```

#### 暱稱重複

- Body:

```json
{
  "result": false,
  "msg": ["nickname:The nickname is already used."]
}
```

#### MQTT

- nickname:加入學生暱稱
- course_stu_total:線上學生人數

```json
{
  "course_data": "略",
  "status": "course_stu_login",
  "api": "",
  "method": "",
  "course_stu_ids": [],
  "nickname": "\u5c0f\u660e",
  "course_stu_total": 19
}
```

### course_stus/update(POST)-更新課堂學生

#### Request

- Method: **POST**
- URL: `course_stus/update`
- Headers: Content-Type:multipart/form-data
- Path-params:

| 名稱         | 類型   | 說明               | 範例   | 是否必須 |
| :----------- | :----- | :----------------- | :----- | :------- |
| nickname     | string | 姓名               | 王小明 | X        |
| avatar_file  | file   | 照片檔案           |        | X        |
| Bearer Token |        | 有登入的學生必須要 |        | X        |
| token        |        | 訪客學生必須要     |        | X        |

#### Response

-成功

- Body:

```json
{
  "result": true,
  "msg": ["Success"],
  "data": []
}
```

-失敗

#### 暱稱重複

- Body:

```json
{
  "result": false,
  "msg": ["nickname:The nickname is already used."]
}
```

### course_stus/get_avatars(POST)-取得課堂學生大頭貼

#### Request

- Method: **POST**
- URL: `course_stus/get_avatars`
- Headers: Content-Type:multipart/form-data
- Path-params:

| 名稱     | 類型  | 說明        | 範例      | 是否必須 |
| :------- | :---- | :---------- | :-------- | :------- |
| students | array | 對象學生 ID | [1, 2, 3] | X        |

#### Response

-成功

- Body:

```json
{
  "result": true,
  "msg": ["Success"],
  "data": {
    "avatar_info": [
      {
        "id": 13,
        "nickname": "min",
        "avatar_file": {
          "id": 132,
          "uploader_id": 0,
          "uploader_type": "student",
          "file_type": "image",
          "course_id": 1,
          "drive_id": "/storage/NtjJqm055RMSkhZsA5I722tknId4beHEA1XNnGfz.png",
          "created_at": "2024-02-24 12:00:14",
          "updated_at": "2024-02-24 12:00:14",
          "deleted_at": null
        }
      },
      {
        "id": 20,
        "nickname": "Alex",
        "avatar_file": {
          "id": 131,
          "uploader_id": 5,
          "uploader_type": "student",
          "file_type": "image",
          "course_id": 1,
          "drive_id": "/storage/PZMFixNRAytUfUqoc0pmyAgH1PDcAbQUG0kv8XTF.png",
          "created_at": "2024-02-24 11:58:33",
          "updated_at": "2024-02-24 11:58:33",
          "deleted_at": null
        }
      }
    ]
  }
}
```

-失敗

#### 暱稱重複

- Body:

```json
{
  "result": false,
  "msg": ["nickname:The nickname is already used."]
}
```

### course_score_logs/create(POST)-幫課堂學生分組加減分

#### Request

- Method: **POST**
- URL: `course_score_logs/create`
- Headers: Content-Type:multipart/form-data
- Path-params:

| 名稱          | 類型   | 說明                                | 範例   | 是否必須 |
| :------------ | :----- | :---------------------------------- | :----- | :------- |
| receiver_id   | int    | 加減分對象 ID                       | 1      | O        |
| receiver_type | string | 加減分對象類型(stu/team)            | stu    | O        |
| item_type     | string | 加減分項目(task/quiz/qa/assessment) | quiz   | O        |
| score         | int    | 加減分數                            | 3      | O        |
| comment       | string | 評語                                | 非常好 | X        |
| Bearer Token  |        | 須為老師                            |        | O        |

#### Response

-成功

- Body:

```json
{
  "receiver_id": 1,
  "item_type": "task",
  "score": 5,
  "receiver_type": "stu",
  "comment": "Very good"
}
```

-失敗

### 加分對象不存在

- Body:

```json
{
  "result": false,
  "msg": ["The course student/team not exists.."]
}
```

### 不是該加分對象的老師

- Body:

```json
{
  "result": false,
  "msg": ["You are not the teacher of the receiver."]
}
```

### 課堂串流-MQTT

#### 教師:課堂串流 MQTT

| 時機                                           | status        | api                        | method | 課堂串流 is_active |
| :--------------------------------------------- | :------------ | :------------------------- | :----- | :----------------- |
| 老師執行 API `course_streams/create` 成功後    | stream        | `course_streams/{id}`(GET) | get    | 1                  |
| 老師執行 API `course_streams/{id}`(PUT) 成功後 | stream_update | `course_streams/{id}`(GET) | get    | 1 /0               |

#### 學生:課堂快問快答學生取得個人化狀態

| 時機說明                 | status         | api                                       | method | 課堂快問快答 is_active |
| :----------------------- | :------------- | :---------------------------------------- | :----- | :--------------------- |
| 建立串流                    | stream    | `course_streams/{id}`(GET)     | get    |                                 |        | 0                      |
| 串流狀態更新            | stream_update |  `course_streams/{id}`(GET)    | post   |  1 /0                     |


### course_streams/create(POST)-建立課堂串流

#### Request

- Method: **POST**
- URL: `course_streams/create`
- Headers: Content-Type:multipart/form-data
- Path-params:

| 名稱         | 類型   | 說明                                             | 範例      | 是否必須 |
| :----------- | :----- | :----------------------------------------------- | :-------- | :------- |
| course_id    | int    | 課堂 ID                                          | 1         | O        |
| stream_type  | string | 值可為 broadcast(廣播),mirror(鏡像),camera(鏡頭) | broadcast | O        |
| students     | array  | 對象學生 ID                                      | [1, 2, 3] | O        |
| Bearer Token |        | 要為老師身分才可建立                             |           | O        |

#### Response

-成功

- Body:

```json
{
  "result": true,
  "msg": ["Success"],
  "data": {
    "id": 10,
    "url": "3qYaadj1CK"
  }
}
```

-失敗

#### 沒有權限(不是老師)

- Status: 403 Forbidden
- Body:

```json
{
  "result": false,
  "msg": ["You do not have permission to access this resource."]
}
```

#### MQTT

```json
{
  "course_data": "略",
  "status": "stream",
  "api": "course_streams/{id}",
  "method": "get",
  "course_stu_ids": [對象學生ID]
}
```

### course_streams/{id}(PUT)-更新課堂串流

#### Request

- Method: **PUT**
- URL: `course_streams/{id}`
- Headers: Content-Type:multipart/form-data
- Path-params:

| 名稱         | 類型    | 說明                 | 範例 | 是否必須 |
| :----------- | :------ | :------------------- | :--- | :------- |
| is_speakable | boolean | 是否靜音             | 0    | X        |
| is_drawable  | boolean | 學生是否可畫筆       |      | X        |
| is_active    | boolean | 是否啟用串流         | 0    | X        |
| Bearer Token |         | 要為老師身分才可建立 |      | O        |

#### Response

-成功

- Body:

```json
{
  "result": true,
  "msg": ["Success"],
  "data": []
}
```

-失敗

#### 沒有權限(不是老師)

- Status: 403 Forbidden
- Body:

```json
{
  "result": false,
  "msg": ["You do not have permission to access this resource."]
}
```

#### MQTT

```json
{
  "course_data": "略",
  "status": "stream_update",
  "api": "course_streams/{id}",
  "method": "get",
  "course_stu_ids": [對象學生ID]
}
```

### course_streams/{id}?token={token}&force_get={force_get}(GET)-取得課堂串流資料

#### Request

- Method: **GET**
- URL: `course_streams/{id}?token={token}&force_get={force_get}`
- Headers:
- Path-params:

| 名稱         | 類型    | 說明                       | 範例                                | 是否必須 |
| :----------- | :------ | :------------------------- | :---------------------------------- | :------- |
| id           | int     | 課堂串流 ID /或課堂碼 code | 1                                   | O        |
| Bearer Token |         | 有登入的學生必須要         |                                     | X        |
| token        |         | 訪客學生必須要             | 10-d401f35993b3f038d24c552b9b3c3a53 | X        |
| force_get    | boolean | 無論有沒有更新都要取得資料 | 1                                   | X        |

#### Response

-成功

#### 有新資料 或 force_get=1 或 是老師

- Body:

```json
{
  "result": true,
  "msg": ["Success"],
  "data": {
    "id": 12,
    "course_id": 1,
    "is_speakable": "0",
    "is_drawable": "0",
    "url": "kIdMDh5KOM",
    "stream_type": "broadcast",
    "is_active": "1",
    "created_at": "2024-01-03 17:02:05",
    "updated_at": "2024-01-03 17:02:05",
    "deleted_at": null
  }
}
```

#### 上次取得資料到此次沒有更新

```json
{
  "result": true,
  "msg": ["Success"],
  "data": ["Nothing update."]
}
```

-失敗

#### 課堂串流不存在

- Status: 404 Not Found
- Body
  {
  "result": false,
  "msg": [
  "CourseStream with id 13 not found."
  ]
  }

#### 課堂串流已關閉

- Body

```json
{
  "result": false,
  "msg": ["Course stream is not active."]
}
```

### 課堂快問快答-MQTT/取得學生個人化狀態說明

#### 教師:課堂快問快答發送 MQTT

| 時機                                                          | status         | api                                          | method | 課堂快問快答 is_active |
| :------------------------------------------------------------ | :------------- | :------------------------------------------- | :----- | :--------------------- |
| 老師執行 API `course_quizzes/create` 成功後                   | quiz           | `course_quizzes/{id}/actions/get_stu_status` | get    | 1                      |
| 老師執行 API `course_quizzes/{id}` 將 is_active 設成 false 後 | quiz_closed    |                                              |        | 0                      |
| 老師執行 API `course_quizzes/{id}/actions/correct` 成功後     | quiz_corrected | `course_quizzes/{id}/actions/get_correct`    | get    | 1                      |

#### 學生:課堂快問快答學生取得個人化狀態

| 時機說明                 | status         | api                                       | method | 課堂快問快答 is_active |
| :----------------------- | :------------- | :---------------------------------------- | :----- | :--------------------- |
| 快問快答未開始/已結束    | quiz_closed    |                                           |        | 0                      |
| 學生還沒回答             | quiz_answering | `course_quizzes/{id}/actions/answer `     | post   | 1                      |
| 學生已回答               | quiz_answered  |                                           |        | 1                      |
| 快問快答已被老師批改完成 | quiz_corrected | `course_quizzes/{id}/actions/get_correct` | get    | 1                      |

### course_quizzes/create(POST)-建立課堂快問快答

#### Request

- Method: **POST**
- URL: `course_quizzes/create`
- Headers: Content-Type:multipart/form-data
- Path-params:

| 名稱         | 類型 | 說明                 | 範例 | 是否必須 |
| :----------- | :--- | :------------------- | :--- | :------- |
| course_id    | int  | 課堂 id              | 1    | O        |
| quiz_file    | file | 快問快答題目圖片     |      | O        |
| Bearer Token |      | 要為老師身分才可建立 |      | O        |

#### Response

-成功

- Body:

```json
{
  "result": true,
  "msg": ["Success"],
  "data": {
    "id": 11
  }
}
```

-失敗

#### 沒有權限(不是老師)

- Status: 403 Forbidden
- Body:

```json
{
  "result": false,
  "msg": ["You do not have permission to access this resource."]
}
```

### course_quizzes/{id}(POST)-更新課堂快問快答

#### Request

- Method: **POST**
- URL: `course_quizzes/{id}`
- Headers: Content-Type:multipart/form-data
- Path-params:

| 名稱         | 類型    | 說明                 | 範例 | 是否必須 |
| :----------- | :------ | :------------------- | :--- | :------- |
| quiz_file    | file    | 快問快答題目圖片     |      | X        |
| is_active    | boolean | 是否啟用             | 0    | X        |
| Bearer Token |         | 要為老師身分才可建立 |      | O        |

#### Response

-成功

- Body:

```json
{
  "result": true,
  "msg": ["Success"],
  "data": []
}
```

-失敗

#### 沒有權限(不是老師)

- Status: 403 Forbidden
- Body:

```json
{
  "result": false,
  "msg": ["You do not have permission to access this resource."]
}
```

#### MQTT (若更新 is_active 為 false)

```json
{
  "course_data": "略",
  "status": "quiz_closed",
  "api": "",
  "method": "",
  "course_stu_ids": []
}
```

### course_quizzes/{id}?token={token}&force_get={force_get}(GET)-取得課堂快問快答資料

#### Request

- Method: **GET**
- URL: `course_quizzes/{id}?token={token}&force_get={force_get}`
- Headers:
- Path-params:

| 名稱         | 類型    | 說明                        | 範例 | 是否必須 |
| :----------- | :------ | :-------------------------- | :--- | :------- |
| id           | int     | 課堂快問快答 ID             | 1    | O        |
| token        | string  | 課堂學生 ID(訪客學生必須要) | 1    | X        |
| Bearer Token |         | 有登入的學生必/老師須要     |      | X        |
| force_get    | boolean | 無論有沒有更新都要取得資料  | 1    | X        |

#### Response

-成功

### 有新資料 或 force_get=1 或 是老師

- Body:

```json
{
  "result": true,
  "msg": ["Success"],
  "data": {
    "course_quiz": {
      "id": 12,
      "course_id": 1,
      "quiz_file_id": 16,
      "is_active": "1",
      "created_at": "2024-01-06 18:28:38",
      "updated_at": "2024-01-06 18:28:38",
      "deleted_at": null,
      "quiz_file": {
        "id": 16,
        "uploader_id": 2,
        "uploader_type": "teacher",
        "file_type": "image",
        "course_id": 1,
        "drive_id": "9UcWx1bMRcqie0YJ8McHuoPZfPCWTh4Ni1CwXmom.png",
        "created_at": "2024-01-06 18:28:38",
        "updated_at": "2024-01-06 18:28:38",
        "deleted_at": null
      },
      "course": {
        "id": 1,
        "user_id": 2,
        "class_name": "一年一班",
        "subject": "數學",
        "code": "yMdlXBrpo9",
        "is_open": 1,
        "status": "quiz",
        "created_at": "2023-12-28 11:15:04",
        "updated_at": "2024-01-06 18:28:38",
        "deleted_at": null,
        "status_id": 12,
        "qrcode_svg": "<?xml version=\"1.0\" encoding=\"UTF-8\"?>\n<svg xmlns=\"http://www.w3.org/2000/svg\" version=\"1.1\" width=\"100\" height=\"100\" viewBox=\"0 0 100 100\"><rect x=\"0\" y=\"0\" width=\"100\" height=\"100\" fill=\"#ffffff\"/><g transform=\"scale(4.762)\"><g transform=\"translate(0,0)\"><path fill-rule=\"evenodd\" d=\"M8 0L8 1L9 1L9 2L8 2L8 5L11 5L11 4L12 4L12 3L13 3L13 0L12 0L12 3L11 3L11 2L10 2L10 0ZM9 2L9 4L11 4L11 3L10 3L10 2ZM8 6L8 7L9 7L9 8L8 8L8 9L9 9L9 10L6 10L6 9L7 9L7 8L6 8L6 9L4 9L4 8L0 8L0 9L1 9L1 10L0 10L0 11L3 11L3 12L2 12L2 13L8 13L8 14L9 14L9 16L10 16L10 17L8 17L8 21L9 21L9 19L10 19L10 17L12 17L12 16L13 16L13 19L12 19L12 18L11 18L11 21L14 21L14 20L15 20L15 19L14 19L14 18L15 18L15 17L14 17L14 16L13 16L13 15L11 15L11 13L12 13L12 12L13 12L13 9L14 9L14 8L13 8L13 9L12 9L12 12L10 12L10 14L9 14L9 12L8 12L8 11L9 11L9 10L10 10L10 9L11 9L11 6L10 6L10 7L9 7L9 6ZM12 6L12 7L13 7L13 6ZM9 8L9 9L10 9L10 8ZM16 8L16 10L14 10L14 11L16 11L16 10L18 10L18 9L19 9L19 8ZM20 8L20 9L21 9L21 8ZM2 9L2 10L3 10L3 11L4 11L4 9ZM19 10L19 11L21 11L21 10ZM6 11L6 12L7 12L7 11ZM17 11L17 12L18 12L18 11ZM0 12L0 13L1 13L1 12ZM14 12L14 13L13 13L13 14L14 14L14 15L15 15L15 16L17 16L17 17L16 17L16 18L18 18L18 19L19 19L19 18L20 18L20 17L19 17L19 15L17 15L17 13L16 13L16 12ZM20 12L20 13L19 13L19 14L20 14L20 13L21 13L21 12ZM14 13L14 14L15 14L15 13ZM20 15L20 16L21 16L21 15ZM13 19L13 20L14 20L14 19ZM20 19L20 20L21 20L21 19ZM17 20L17 21L18 21L18 20ZM0 0L0 7L7 7L7 0ZM1 1L1 6L6 6L6 1ZM2 2L2 5L5 5L5 2ZM14 0L14 7L21 7L21 0ZM15 1L15 6L20 6L20 1ZM16 2L16 5L19 5L19 2ZM0 14L0 21L7 21L7 14ZM1 15L1 20L6 20L6 15ZM2 16L2 19L5 19L5 16Z\" fill=\"#000000\"/></g></g></svg>\n"
      }
    },
    "course_stu_quiz_id": 1
  }
}
```

### 上次取得資料到此次沒有更新(只限學生)

```json
{
  "result": true,
  "msg": ["Success"],
  "data": ["Nothing update."]
}
```

-失敗

### 課堂快問快答不存在

- Status: 404 Not Found
- Body

```json
{
  "result": false,
  "msg": ["CourseQuiz with id 13 not found."]
}
```

### 課堂快問快答已關閉

- Body

```json
{
  "result": false,
  "msg": ["Course quiz is not active."]
}
```

### course_quizzes/{id}/actions/answer(POST)-學生回答快問快答

#### Request

- Method: **POST**
- URL: `course_quizzes/{id}/actions/answer`
- Headers: Content-Type:multipart/form-data
- Path-params:

| 名稱         | 類型 | 說明               | 範例                                | 是否必須 |
| :----------- | :--- | :----------------- | :---------------------------------- | :------- |
| answer_file  | file | 回答快問快答圖片   |                                     | O        |
| Bearer Token |      | 有登入的學生必須要 |                                     | X        |
| token        |      | 訪客學生必須要     | 10-d401f35993b3f038d24c552b9b3c3a53 | X        |

#### Response

-成功

- Body:

```json
{
  "result": true,
  "msg": ["Success"],
  "data": []
}
```

-失敗

#### 沒有權限

- Status: 403 Forbidden
- Body:

```json
{
  "result": false,
  "msg": ["You do not have permission to access this resource."]
}
```

### course_quizzes/{id}/actions/get_answer?course_stu_id={course_stu_id}(GET)-老師取得學生快問快答答案

#### Request

- Method: **GET**
- URL: `course_quizzes/{id}?token={token}&force_get={force_get}`
- Headers:
- Path-params:

| 名稱          | 類型 | 說明            | 範例 | 是否必須                    |
| :------------ | :--- | :-------------- | :--- | :-------------------------- |
| id            | int  | 課堂快問快答 ID | 1    | O                           |
| Bearer Token  |      |                 |      | O                           |
| course_stu_id | int  | 課堂學生 ID     | 1    | X(沒給的話會取得全班的結果) |

#### Response

-成功

- Body:

```json (全班)
{
  "result": true,
  "msg": ["Success"],
  "data": [
    {
      "id": 10,
      "course_quiz_id": 13,
      "course_stu_id": 12,
      "answer_file_id": null,
      "correct_file_id": null,
      "answer_file_type": "",
      "created_at": "2024-02-03 16:31:10",
      "updated_at": "2024-02-03 16:31:10",
      "deleted_at": null,
      "last_seen_at": null,
      "answer_file": null,
      "course_stu": {
        "id": 12,
        "course_id": 1,
        "user_id": 3,
        "nickname": "小明",
        "is_visitor": 0,
        "score": 0,
        "avatar_file_id": 32,
        "is_online": 1,
        "created_at": "2024-01-14 13:46:10",
        "updated_at": "2024-01-14 13:46:10",
        "deleted_at": null,
        "stream_url": null,
        "comment": "",
        "avatar_file": {
          "id": 32,
          "uploader_id": 2,
          "uploader_type": "teacher",
          "file_type": "image",
          "course_id": 1,
          "drive_id": "/storage/het8OkZJOayqSafvFp5PjudHpzEMKoMqg7b0JEcO.png",
          "created_at": "2024-01-06 19:30:06",
          "updated_at": "2024-01-06 19:30:06",
          "deleted_at": null
        }
      }
    },
    {
      "id": 11,
      "course_quiz_id": 13,
      "course_stu_id": 13,
      "answer_file_id": 56,
      "correct_file_id": null,
      "answer_file_type": "",
      "created_at": "2024-02-03 16:31:10",
      "updated_at": "2024-02-03 16:32:52",
      "deleted_at": null,
      "last_seen_at": null,
      "answer_file": {
        "id": 56,
        "uploader_id": 0,
        "uploader_type": "student",
        "file_type": "image",
        "course_id": 1,
        "drive_id": "/storage/nxtUXBjDHUg3wIPDfGSRkOZzPDKDXiu5It5y78Wc.png",
        "created_at": "2024-02-03 16:32:52",
        "updated_at": "2024-02-03 16:32:52",
        "deleted_at": null
      },
      "course_stu": {
        "id": 13,
        "course_id": 1,
        "user_id": 0,
        "nickname": "心心",
        "is_visitor": 1,
        "score": 0,
        "avatar_file_id": 2,
        "is_online": 1,
        "created_at": "2024-01-14 14:31:34",
        "updated_at": "2024-01-14 14:31:34",
        "deleted_at": null,
        "stream_url": null,
        "comment": "",
        "avatar_file": {
          "id": 2,
          "uploader_id": 2,
          "uploader_type": "teacher",
          "file_type": "image",
          "course_id": 1,
          "drive_id": "/storage/3bMh2q7veqawRhojKPbekym3qmf4p7DMvAb4FG8E.png",
          "created_at": "2024-01-05 16:19:46",
          "updated_at": "2024-01-05 16:19:46",
          "deleted_at": null
        }
      }
    },
    {
      "id": 12,
      "course_quiz_id": 13,
      "course_stu_id": 15,
      "answer_file_id": null,
      "correct_file_id": null,
      "answer_file_type": "",
      "created_at": "2024-02-03 16:31:10",
      "updated_at": "2024-02-03 16:31:10",
      "deleted_at": null,
      "last_seen_at": null,
      "answer_file": null,
      "course_stu": {
        "id": 15,
        "course_id": 1,
        "user_id": 0,
        "nickname": "心心",
        "is_visitor": 1,
        "score": 0,
        "avatar_file_id": 5,
        "is_online": 1,
        "created_at": "2024-01-16 22:36:33",
        "updated_at": "2024-01-16 22:36:33",
        "deleted_at": null,
        "stream_url": null,
        "comment": "",
        "avatar_file": {
          "id": 5,
          "uploader_id": 2,
          "uploader_type": "teacher",
          "file_type": "image",
          "course_id": 1,
          "drive_id": "/storage/BJ3pCI1q4AbgWNtpNfQLyU0nKg2rg6Nkd9z3sUM7.png",
          "created_at": "2024-01-05 16:23:54",
          "updated_at": "2024-01-05 16:23:54",
          "deleted_at": null
        }
      }
    }
  ]
}
```

```json (個人)
{
  "result": true,
  "msg": ["Success"],
  "data": {
    "id": 56,
    "uploader_id": 0,
    "uploader_type": "student",
    "file_type": "image",
    "course_id": 1,
    "drive_id": "nxtUXBjDHUg3wIPDfGSRkOZzPDKDXiu5It5y78Wc.png",
    "created_at": "2024-02-03 16:32:52",
    "updated_at": "2024-02-03 16:32:52",
    "deleted_at": null
  }
}
```

-失敗

### 課堂快問快答不存在

- Status: 404 Not Found
- Body

```json
{
  "result": false,
  "msg": ["CourseQuiz with id 13 not found."]
}
```

### 不是該堂課的老師

- Body

```json
{
  "result": false,
  "msg": ["You do not have permission to access this resource."]
}
```

### course_quizzes/{id}/actions/correct(POST)-老師批閱學生快問快答答案

#### Request

- Method: **POST**
- URL: `course_quizzes/{id}/actions/correct`
- Headers: Content-Type:multipart/form-data
- Path-params:

| 名稱          | 類型 | 說明            | 範例 | 是否必須 |
| :------------ | :--- | :-------------- | :--- | :------- |
| id            | int  | 課堂快問快答 ID | 1    | O        |
| correct_file  | file | 批閱圖片        |      | O        |
| course_stu_id | int  | 課堂學生 ID     | 1    | O        |
| Bearer Token  |      |                 |      | O        |

#### Response

-成功

- Body:

```json
{
  "result": true,
  "msg": ["Success"],
  "data": []
}
```

-失敗

#### 沒有權限

- Status: 403 Forbidden
- Body:

```json
{
  "result": false,
  "msg": ["You do not have permission to access this resource."]
}
```

#### MQTT

```json
{
  "course_data": "略",
  "status": "quiz_corrected",
  "api": "course_quizzes/{id}/actions/get_correct",
  "method": "get",
  "course_stu_ids": ["{course_stu_id}"]
}
```

### course_quizzes/{id}/actions/get_correct?token={token}(GET)-學生取得老師快問快答批閱結果

#### Request

- Method: **GET**
- URL: `course_quizzes/{id}/actions/get_correct?token={token}`
- Headers:
- Path-params:

| 名稱         | 類型 | 說明               | 範例                                | 是否必須 |
| :----------- | :--- | :----------------- | :---------------------------------- | :------- |
| id           | int  | 課堂快問快答 ID    | 1                                   | O        |
| Bearer Token |      | 有登入的學生必須要 |                                     | X        |
| token        |      | 訪客學生必須要     | 10-d401f35993b3f038d24c552b9b3c3a53 | X        |

#### Response

-成功

- Body:

```json
{
  "result": true,
  "msg": ["Success"],
  "data": {
    "id": 41,
    "uploader_id": 2,
    "uploader_type": "teacher",
    "file_type": "image",
    "course_id": 1,
    "drive_id": "EZMfc3UivglWTagPebLeQswrTslOoz56G6q25GTu.jpg",
    "created_at": "2024-01-15 14:05:10",
    "updated_at": "2024-01-15 14:05:10",
    "deleted_at": null
  }
}
```

-失敗

#### 課堂快問快答不存在

- Status: 404 Not Found
- Body

```json
{
  "result": false,
  "msg": ["CourseQuiz with id 13 not found."]
}
```

#### 批閱結果不存在

```json
{
  "result": false,
  "msg": ["Correct file not exists."]
}
```

### course_quizzes/{id}/actions/get_stu_status(GET)-取得學生個人課堂快問快答狀態

#### Request

- Method: **GET**
- URL: `course_quizzes/{id}/actions/get_stu_status`
- Headers:
- Path-params:

| 名稱         | 類型 | 說明                    | 範例                                | 是否必須 |
| :----------- | :--- | :---------------------- | :---------------------------------- | :------- |
| id           | int  | 課堂快問快答 ID         | 1                                   | O        |
| Bearer Token |      | 有登入的學生/老師必須要 |                                     | X        |
| token        |      | 訪客學生必須要          | 10-d401f35993b3f038d24c552b9b3c3a53 | X        |

- return-params:

| 名稱   | 類型  | 說明                                        | 範例        |
| :----- | :---- | :------------------------------------------ | :---------- |
| data   | int   | 如 api 是 get 類型，會先傳該 api 回覆的資料 |             |
| status | int   | 除了狀態包含 MQTT 發送的狀態之外            | task_closed |
| api    | int   | api 路徑                                    |             |
| method | array | api 方法                                    |             |

- [回傳內容說明參考](#課堂快問快答學生取得個人化狀態)

#### Response

-成功

- Body:

```json
{
  "result": true,
  "msg": ["Success"],
  "data": {
    "course_quiz": {
      "id": 14,
      "course_id": 1,
      "quiz_file_id": 115,
      "is_active": "1",
      "created_at": "2024-02-20 15:51:22",
      "updated_at": "2024-02-20 15:52:05",
      "deleted_at": null,
      "quiz_file": {
        "id": 115,
        "uploader_id": 2,
        "uploader_type": "teacher",
        "file_type": "image",
        "course_id": 1,
        "drive_id": "/storage/1rfiL663YdpQnDzMoXzK1MsptsacBN2QCgfcJsPY.png",
        "created_at": "2024-02-20 15:52:05",
        "updated_at": "2024-02-20 15:52:05",
        "deleted_at": null
      }
    },
    "course_stu_quiz_id": 20
  },
  "status": "quiz_answering",
  "api": "course_quizzes/14/actions/answer",
  "method": "post"
}
```

-失敗

#### 沒有權限

```json
{
  "result": false,
  "msg": ["You do not have permission to access this resource."]
}
```

### course_deliveries/create(POST)-建立課堂派送

#### Request

- Method: **POST**
- URL: `course_deliveries/create`
- Headers: Content-Type:multipart/form-data
- Path-params:

| 名稱          | 類型   | 說明                                   | 範例                         | 是否必須                            |
| :------------ | :----- | :------------------------------------- | :--------------------------- | :---------------------------------- |
| course_id     | int    | 課堂 id                                | 1                            | O                                   |
| action_type   | string | delivery(派送)/push(推播)              | delivery                     | O                                   |
| delivery_type | string | url/file                               | url                          | O                                   |
| url           | string | 網址                                   | https://www.google.com/      | X(如果 delivery_type 是 url 才必須) |
| file          | file   | 檔案(jpeg,bmp,png,gif,svg,pdf)         |                              | X(如果 file 是 url 才必須)          |
| students      | array  | 對象學生 ID (可選擇輸入這個或 team_id) | [1, 2, 3]                    | X                                   |
| team_id       | int    | 分組 ID                                | 1(可選擇輸入這個或 students) | X                                   |
| Bearer Token  |        | 要為老師身分才可建立                   |                              | O                                   |

#### Response

-成功

- Body:

```json
{
  "result": true,
  "msg": ["Success"],
  "data": {
    "id": 4
  }
}
```

-失敗

#### 沒有權限(不是老師)

- Status: 403 Forbidden
- Body:

```json
{
  "result": false,
  "msg": ["You do not have permission to access this resource."]
}
```

#### MQTT

```json
{
  "course_data": "略",
  "status": "delivery",
  "api": "course_deliveries/{id}",
  "method": "get",
  "course_stu_ids": [{course_stu_ids}]
}
```

### course_deliveries/{id}?token={token}&force_get={force_get}(GET)-取得課堂派送

#### Request

- Method: **GET**
- URL: `course_deliveries/{id}?token={token}&force_get={force_get}`
- Headers:
- Path-params:

| 名稱         | 類型    | 說明                       | 範例                                | 是否必須 |
| :----------- | :------ | :------------------------- | :---------------------------------- | :------- |
| id           | int     | 課堂派送 ID                | 1                                   | O        |
| Bearer Token |         | 有登入的學生必須要         |                                     | X        |
| token        |         | 訪客學生必須要             | 10-d401f35993b3f038d24c552b9b3c3a53 | X        |
| force_get    | boolean | 無論有沒有更新都要取得資料 | 1                                   | X        |

#### Response

-成功

### 未讀 或 force_get=1 或 是老師

- Body:

```json (派送網址)
{
  "result": true,
  "msg": ["Success"],
  "data": {
    "id": 7,
    "course_id": 1,
    "url": "https://stackoverflow.com/questions/39467354/laravel-validation-allow-image-or-pdf",
    "delivery_type": "url",
    "action_type": "delivery",
    "created_at": "2024-01-20 17:18:11",
    "updated_at": "2024-01-20 17:18:11",
    "deleted_at": null,
    "file_id": null
  }
}
```

```json 派送檔案
{
  "result": true,
  "msg": ["Success"],
  "data": {
    "id": 8,
    "course_id": 1,
    "url": null,
    "delivery_type": "file",
    "created_at": "2024-01-20 20:52:35",
    "updated_at": "2024-01-20 20:52:35",
    "deleted_at": null,
    "file_id": 42,
    "file": {
      "id": 42,
      "uploader_id": 2,
      "uploader_type": "teacher",
      "file_type": "",
      "course_id": 1,
      "drive_id": "AQ4EIPv9wQ1BKgYWQqzWNIFdrcO8EnZQ4gpqtyLB.png",
      "created_at": "2024-01-20 20:52:35",
      "updated_at": "2024-01-20 20:52:35",
      "deleted_at": null
    }
  }
}
```

### 已經讀過了

```json
{
  "result": true,
  "msg": ["Success"],
  "data": ["Already read."]
}
```

-失敗

### 課堂派送不存在

- Status: 404 Not Found
- Body

```json
{
  "result": false,
  "msg": ["CourseDelivery with id 8 not found."]
}
```

#### 沒有權限

```json
{
  "result": false,
  "msg": ["You do not have permission to access this resource."]
}
```

### 課堂分組-MQTT

#### 教師:課堂分組發送 MQTT

| 時機                                            | status       | api                    | method |
| :---------------------------------------------- | :----------- | :--------------------- | :----- |
| 老師執行 API `course_teams/create` 成功後       | team         | `course_teams/my`(GET) | get    |
| 老師執行 API `course_teams/{id}`(PUT) 成功後    | team_update  | `course_teams/my`(GET) | get    |
| 老師執行 API `course_teams/{id}`(DELETE) 成功後 | team_deleted | `course_teams/my`(GET) | get    |

#### 學生:課堂分組發送 MQTT
無須反映

### course_teams/create(POST)-建立課堂分組

#### Request

- Method: **POST**
- URL: `course_teams/create`
- Headers: Content-Type:multipart/form-data
- Path-params:

| 名稱         | 類型   | 說明                 | 範例      | 是否必須 |
| :----------- | :----- | :------------------- | :-------- | :------- |
| course_id    | int    | 課堂 id              | 1         | O        |
| name         | string | 組名                 | A         | O        |
| leader_id    | int    | 組長 ID              | 1         | O        |
| students     | array  | 對象學生 ID          | [1, 2, 3] | O        |
| Bearer Token |        | 要為老師身分才可建立 |           | O        |

#### Response

-成功

- Body:

```json
{
  "result": true,
  "msg": ["Success"],
  "data": {
    "id": 2
  }
}
```

-失敗

#### 沒有權限(不是老師)

- Status: 403 Forbidden
- Body:

```json
{
  "result": false,
  "msg": ["You do not have permission to access this resource."]
}
```

#### MQTT

```json
{
  "course_data": "略",
  "status": "team",
  "api": "course_teams/my",
  "method": "get",
  "course_stu_ids": []
}
```

### course_teams/{id}(PUT)-更新課堂分組

#### Request

- Method: **PUT**
- URL: `course_teams/{id}`
- Headers: Content-Type:multipart/form-data
- Path-params:

| 名稱         | 類型   | 說明                 | 範例      | 是否必須 |
| :----------- | :----- | :------------------- | :-------- | :------- |
| id           | int    | 課堂分組 id          | 1         | O        |
| name         | string | 組名                 | A         | X        |
| leader_id    | int    | 組長 ID              | 1         | X        |
| students     | array  | 對象學生 ID          | [1, 2, 3] | X        |
| Bearer Token |        | 要為老師身分才可建立 |           | O        |

#### Response

-成功

- Body:

```json
{
  "result": true,
  "msg": ["Success"],
  "data": {
    "id": 17
  }
}
```

-失敗

#### 沒有權限(不是老師)

- Status: 403 Forbidden
- Body:

```json
{
  "result": false,
  "msg": ["You do not have permission to access this resource."]
}
```

#### 組長 id 不在分組中

```json
{
  "result": false,
  "msg": ["Leader's id not in the team."]
}
```

#### MQTT

```json
{
  "course_data": "略",
  "status": "team_update",
  "api": "course_teams/my",
  "method": "get",
  "course_stu_ids": []
}
```

### course_teams/{id}(DELETE)-刪除課堂分組

#### Request

- Method: **DELETE**
- URL: `course_teams/{id}`
- Headers: Content-Type:multipart/form-data
- Path-params:

| 名稱         | 類型 | 說明                 | 範例 | 是否必須 |
| :----------- | :--- | :------------------- | :--- | :------- |
| id           | int  | 課堂分組 id          | 1    | O        |
| Bearer Token |      | 要為老師身分才可建立 |      | O        |

#### Response

-成功

- Body:

```json
{
  "result": true,
  "msg": ["Success"],
  "data": []
}
```

-失敗

#### 沒有權限(不是老師)

- Status: 403 Forbidden
- Body:

```json
{
  "result": false,
  "msg": ["You do not have permission to access this resource."]
}
```

#### 找不到課堂分組

```json
{
  "result": false,
  "msg": ["CourseTeam with id 17 not found."]
}
```

#### MQTT

```json
{
  "course_data": "略",
  "status": "team_deleted",
  "api": "course_teams/my",
  "method": "get",
  "course_stu_ids": []
}
```

### courses/{id}/course_teams/random_create(POST)-建立隨機課堂分組

#### Request

- Method: **POST**
- URL: `courses/{id}/course_teams/random_create`
- Headers: Content-Type:multipart/form-data
- Path-params:

| 名稱         | 類型 | 說明                 | 範例 | 是否必須 |
| :----------- | :--- | :------------------- | :--- | :------- |
| course_id    | int  | 課堂 id              | 1    | O        |
| team_number  | int  | 分成幾組個數         | 5    | O        |
| Bearer Token |      | 要為老師身分才可建立 |      | O        |

#### Response

-成功

- Body:

```json
{
  "result": true,
  "msg": ["Success"],
  "data": [
    {
      "id": 68,
      "name": "A",
      "score": 0,
      "course_id": 1,
      "whiteboard_url": "url",
      "created_at": "2024-03-09 13:16:23",
      "updated_at": "2024-03-09 13:16:23",
      "deleted_at": null,
      "course_stu_teams": [
        {
          "id": 163,
          "course_stu_id": 16,
          "course_team_id": 68,
          "is_leader": 1,
          "created_at": "2024-03-09 13:16:23",
          "updated_at": "2024-03-09 13:16:23",
          "deleted_at": null,
          "course_stu": {
            "id": 16,
            "course_id": 1,
            "user_id": 3,
            "nickname": "王晶晶3",
            "is_visitor": 0,
            "score": 0,
            "avatar_file_id": 0,
            "is_online": 1,
            "created_at": "2024-02-23 12:35:27",
            "updated_at": "2024-02-23 12:35:27",
            "deleted_at": null,
            "stream_url": null,
            "comment": ""
          }
        },
        {
          "id": 164,
          "course_stu_id": 24,
          "course_team_id": 68,
          "is_leader": 0,
          "created_at": "2024-03-09 13:16:23",
          "updated_at": "2024-03-09 13:16:23",
          "deleted_at": null,
          "course_stu": {
            "id": 24,
            "course_id": 1,
            "user_id": 0,
            "nickname": "小名5",
            "is_visitor": 1,
            "score": 0,
            "avatar_file_id": 0,
            "is_online": 1,
            "created_at": "2024-03-03 15:30:53",
            "updated_at": "2024-03-03 15:30:53",
            "deleted_at": null,
            "stream_url": null,
            "comment": ""
          }
        },
        {
          "id": 165,
          "course_stu_id": 17,
          "course_team_id": 68,
          "is_leader": 0,
          "created_at": "2024-03-09 13:16:23",
          "updated_at": "2024-03-09 13:16:23",
          "deleted_at": null,
          "course_stu": {
            "id": 17,
            "course_id": 1,
            "user_id": 3,
            "nickname": "王晶晶",
            "is_visitor": 0,
            "score": 0,
            "avatar_file_id": 0,
            "is_online": 1,
            "created_at": "2024-02-23 12:36:13",
            "updated_at": "2024-02-23 12:36:13",
            "deleted_at": null,
            "stream_url": null,
            "comment": ""
          }
        },
        {
          "id": 166,
          "course_stu_id": 23,
          "course_team_id": 68,
          "is_leader": 0,
          "created_at": "2024-03-09 13:16:23",
          "updated_at": "2024-03-09 13:16:23",
          "deleted_at": null,
          "course_stu": {
            "id": 23,
            "course_id": 1,
            "user_id": 0,
            "nickname": "小名4",
            "is_visitor": 1,
            "score": 0,
            "avatar_file_id": 0,
            "is_online": 1,
            "created_at": "2024-03-03 15:30:21",
            "updated_at": "2024-03-03 15:30:21",
            "deleted_at": null,
            "stream_url": null,
            "comment": ""
          }
        },
        {
          "id": 167,
          "course_stu_id": 7,
          "course_team_id": 68,
          "is_leader": 0,
          "created_at": "2024-03-09 13:16:23",
          "updated_at": "2024-03-09 13:16:23",
          "deleted_at": null,
          "course_stu": {
            "id": 7,
            "course_id": 1,
            "user_id": 3,
            "nickname": "晶晶",
            "is_visitor": 0,
            "score": 0,
            "avatar_file_id": 1,
            "is_online": 1,
            "created_at": "2024-01-03 17:23:21",
            "updated_at": "2024-01-03 17:23:21",
            "deleted_at": null,
            "stream_url": null,
            "comment": ""
          }
        },
        {
          "id": 168,
          "course_stu_id": 25,
          "course_team_id": 68,
          "is_leader": 0,
          "created_at": "2024-03-09 13:16:23",
          "updated_at": "2024-03-09 13:16:23",
          "deleted_at": null,
          "course_stu": {
            "id": 25,
            "course_id": 1,
            "user_id": 0,
            "nickname": "小名12",
            "is_visitor": 1,
            "score": 0,
            "avatar_file_id": 0,
            "is_online": 1,
            "created_at": "2024-03-03 15:32:02",
            "updated_at": "2024-03-03 15:32:02",
            "deleted_at": null,
            "stream_url": null,
            "comment": ""
          }
        }
      ]
    },
    {
      "id": 69,
      "name": "B",
      "score": 0,
      "course_id": 1,
      "whiteboard_url": "url",
      "created_at": "2024-03-09 13:16:23",
      "updated_at": "2024-03-09 13:16:23",
      "deleted_at": null,
      "course_stu_teams": [
        {
          "id": 169,
          "course_stu_id": 18,
          "course_team_id": 69,
          "is_leader": 1,
          "created_at": "2024-03-09 13:16:23",
          "updated_at": "2024-03-09 13:16:23",
          "deleted_at": null,
          "course_stu": {
            "id": 18,
            "course_id": 1,
            "user_id": 3,
            "nickname": "王晶晶3",
            "is_visitor": 0,
            "score": 0,
            "avatar_file_id": 0,
            "is_online": 1,
            "created_at": "2024-02-23 12:36:28",
            "updated_at": "2024-02-23 12:36:28",
            "deleted_at": null,
            "stream_url": null,
            "comment": ""
          }
        },
        {
          "id": 170,
          "course_stu_id": 4,
          "course_team_id": 69,
          "is_leader": 0,
          "created_at": "2024-03-09 13:16:23",
          "updated_at": "2024-03-09 13:16:23",
          "deleted_at": null,
          "course_stu": {
            "id": 4,
            "course_id": 1,
            "user_id": 0,
            "nickname": "小火",
            "is_visitor": 1,
            "score": 0,
            "avatar_file_id": 1,
            "is_online": 1,
            "created_at": "2023-12-30 11:39:56",
            "updated_at": "2024-02-23 11:47:16",
            "deleted_at": null,
            "stream_url": null,
            "comment": ""
          }
        },
        {
          "id": 171,
          "course_stu_id": 19,
          "course_team_id": 69,
          "is_leader": 0,
          "created_at": "2024-03-09 13:16:23",
          "updated_at": "2024-03-09 13:16:23",
          "deleted_at": null,
          "course_stu": {
            "id": 19,
            "course_id": 1,
            "user_id": 0,
            "nickname": "小名",
            "is_visitor": 1,
            "score": 0,
            "avatar_file_id": 0,
            "is_online": 1,
            "created_at": "2024-02-23 12:39:25",
            "updated_at": "2024-02-23 12:39:25",
            "deleted_at": null,
            "stream_url": null,
            "comment": ""
          }
        },
        {
          "id": 172,
          "course_stu_id": 22,
          "course_team_id": 69,
          "is_leader": 0,
          "created_at": "2024-03-09 13:16:23",
          "updated_at": "2024-03-09 13:16:23",
          "deleted_at": null,
          "course_stu": {
            "id": 22,
            "course_id": 1,
            "user_id": 0,
            "nickname": "小名3",
            "is_visitor": 1,
            "score": 0,
            "avatar_file_id": 0,
            "is_online": 1,
            "created_at": "2024-03-03 15:28:50",
            "updated_at": "2024-03-03 15:28:50",
            "deleted_at": null,
            "stream_url": null,
            "comment": ""
          }
        },
        {
          "id": 173,
          "course_stu_id": 20,
          "course_team_id": 69,
          "is_leader": 0,
          "created_at": "2024-03-09 13:16:23",
          "updated_at": "2024-03-09 13:16:23",
          "deleted_at": null,
          "course_stu": {
            "id": 20,
            "course_id": 1,
            "user_id": 5,
            "nickname": "Alex",
            "is_visitor": 0,
            "score": 0,
            "avatar_file_id": 131,
            "is_online": 1,
            "created_at": "2024-02-24 11:52:53",
            "updated_at": "2024-02-24 11:58:33",
            "deleted_at": null,
            "stream_url": null,
            "comment": ""
          }
        },
        {
          "id": 174,
          "course_stu_id": 5,
          "course_team_id": 69,
          "is_leader": 0,
          "created_at": "2024-03-09 13:16:23",
          "updated_at": "2024-03-09 13:16:23",
          "deleted_at": null,
          "course_stu": {
            "id": 5,
            "course_id": 1,
            "user_id": 0,
            "nickname": "小土",
            "is_visitor": 1,
            "score": 0,
            "avatar_file_id": 1,
            "is_online": 1,
            "created_at": "2023-12-30 13:06:05",
            "updated_at": "2024-02-23 11:47:16",
            "deleted_at": null,
            "stream_url": null,
            "comment": ""
          }
        }
      ]
    },
    {
      "id": 70,
      "name": "C",
      "score": 0,
      "course_id": 1,
      "whiteboard_url": "url",
      "created_at": "2024-03-09 13:16:23",
      "updated_at": "2024-03-09 13:16:23",
      "deleted_at": null,
      "course_stu_teams": [
        {
          "id": 175,
          "course_stu_id": 21,
          "course_team_id": 70,
          "is_leader": 1,
          "created_at": "2024-03-09 13:16:23",
          "updated_at": "2024-03-09 13:16:23",
          "deleted_at": null,
          "course_stu": {
            "id": 21,
            "course_id": 1,
            "user_id": 0,
            "nickname": "小名2",
            "is_visitor": 1,
            "score": 0,
            "avatar_file_id": 0,
            "is_online": 1,
            "created_at": "2024-03-03 15:23:13",
            "updated_at": "2024-03-03 15:23:13",
            "deleted_at": null,
            "stream_url": null,
            "comment": ""
          }
        },
        {
          "id": 176,
          "course_stu_id": 11,
          "course_team_id": 70,
          "is_leader": 0,
          "created_at": "2024-03-09 13:16:23",
          "updated_at": "2024-03-09 13:16:23",
          "deleted_at": null,
          "course_stu": {
            "id": 11,
            "course_id": 1,
            "user_id": 0,
            "nickname": "心心",
            "is_visitor": 1,
            "score": 0,
            "avatar_file_id": 3,
            "is_online": 1,
            "created_at": "2024-01-14 13:40:45",
            "updated_at": "2024-01-14 13:40:45",
            "deleted_at": null,
            "stream_url": null,
            "comment": ""
          }
        },
        {
          "id": 177,
          "course_stu_id": 13,
          "course_team_id": 70,
          "is_leader": 0,
          "created_at": "2024-03-09 13:16:23",
          "updated_at": "2024-03-09 13:16:23",
          "deleted_at": null,
          "course_stu": {
            "id": 13,
            "course_id": 1,
            "user_id": 0,
            "nickname": "min",
            "is_visitor": 1,
            "score": 0,
            "avatar_file_id": 132,
            "is_online": 1,
            "created_at": "2024-01-14 14:31:34",
            "updated_at": "2024-02-24 12:00:14",
            "deleted_at": null,
            "stream_url": null,
            "comment": ""
          }
        },
        {
          "id": 178,
          "course_stu_id": 12,
          "course_team_id": 70,
          "is_leader": 0,
          "created_at": "2024-03-09 13:16:23",
          "updated_at": "2024-03-09 13:16:23",
          "deleted_at": null,
          "course_stu": {
            "id": 12,
            "course_id": 1,
            "user_id": 3,
            "nickname": "小明",
            "is_visitor": 0,
            "score": 0,
            "avatar_file_id": 32,
            "is_online": 1,
            "created_at": "2024-01-14 13:46:10",
            "updated_at": "2024-01-14 13:46:10",
            "deleted_at": null,
            "stream_url": null,
            "comment": ""
          }
        },
        {
          "id": 179,
          "course_stu_id": 10,
          "course_team_id": 70,
          "is_leader": 0,
          "created_at": "2024-03-09 13:16:23",
          "updated_at": "2024-03-09 13:16:23",
          "deleted_at": null,
          "course_stu": {
            "id": 10,
            "course_id": 1,
            "user_id": 0,
            "nickname": "心心",
            "is_visitor": 1,
            "score": 0,
            "avatar_file_id": 4,
            "is_online": 1,
            "created_at": "2024-01-13 17:25:22",
            "updated_at": "2024-01-13 17:25:22",
            "deleted_at": null,
            "stream_url": null,
            "comment": ""
          }
        },
        {
          "id": 180,
          "course_stu_id": 15,
          "course_team_id": 70,
          "is_leader": 0,
          "created_at": "2024-03-09 13:16:23",
          "updated_at": "2024-03-09 13:16:23",
          "deleted_at": null,
          "course_stu": {
            "id": 15,
            "course_id": 1,
            "user_id": 0,
            "nickname": "心心",
            "is_visitor": 1,
            "score": 0,
            "avatar_file_id": 5,
            "is_online": 1,
            "created_at": "2024-01-16 22:36:33",
            "updated_at": "2024-01-16 22:36:33",
            "deleted_at": null,
            "stream_url": null,
            "comment": ""
          }
        },
        {
          "id": 181,
          "course_stu_id": 9,
          "course_team_id": 70,
          "is_leader": 0,
          "created_at": "2024-03-09 13:16:23",
          "updated_at": "2024-03-09 13:16:23",
          "deleted_at": null,
          "course_stu": {
            "id": 9,
            "course_id": 1,
            "user_id": 0,
            "nickname": "甜甜",
            "is_visitor": 1,
            "score": 0,
            "avatar_file_id": 2,
            "is_online": 1,
            "created_at": "2024-01-04 12:00:57",
            "updated_at": "2024-01-04 12:00:57",
            "deleted_at": null,
            "stream_url": null,
            "comment": ""
          }
        }
      ]
    }
  ]
}
```

-失敗

#### 沒有權限(不是老師)

- Status: 403 Forbidden
- Body:

```json
{
  "result": false,
  "msg": ["You do not have permission to access this resource."]
}
```

#### MQTT

```json
{
  "course_data": "略",
  "status": "team",
  "api": "course_teams/my",
  "method": "get",
  "course_stu_ids": []
}
```

### courses/{id}/course_teams(GET)-取得所有課堂分組

#### Request

- Method: **GET**
- URL: `courses/{id}/course_teams`
- Headers:
- Path-params:

| 名稱         | 類型 | 說明                   | 範例 | 是否必須 |
| :----------- | :--- | :--------------------- | :--- | :------- |
| id           | int  | 課堂 ID                | 1    | O        |
| Bearer Token |      | 只有老師可以取得所有的 |      | O        |

#### Response

-成功

- Body:

```json
{
  "result": true,
  "msg": ["Success"],
  "data": [
    {
      "id": 1,
      "name": "A",
      "score": 0,
      "course_id": 1,
      "whiteboard_url": "url",
      "created_at": "2024-01-20 22:52:11",
      "updated_at": "2024-01-20 22:52:11",
      "deleted_at": null,
      "course_stu_teams": [
        {
          "id": 1,
          "course_stu_id": 1,
          "course_team_id": 1,
          "is_leader": 1,
          "created_at": "2024-01-20 22:52:11",
          "updated_at": "2024-01-20 22:52:11",
          "deleted_at": null,
          "course_stu": {
            "id": 1,
            "course_id": 1,
            "user_id": 0,
            "nickname": "小金",
            "is_visitor": 1,
            "score": 15,
            "avatar_file_id": 1,
            "is_online": 0,
            "created_at": "2023-12-29 09:24:06",
            "updated_at": "2024-01-20 11:45:09",
            "deleted_at": null,
            "stream_url": null,
            "comment": "表現優異"
          }
        },
        {
          "id": 2,
          "course_stu_id": 7,
          "course_team_id": 1,
          "is_leader": 0,
          "created_at": "2024-01-20 22:52:11",
          "updated_at": "2024-01-20 22:52:11",
          "deleted_at": null,
          "course_stu": {
            "id": 7,
            "course_id": 1,
            "user_id": 3,
            "nickname": "晶晶",
            "is_visitor": 0,
            "score": 0,
            "avatar_file_id": 0,
            "is_online": 1,
            "created_at": "2024-01-03 17:23:21",
            "updated_at": "2024-01-03 17:23:21",
            "deleted_at": null,
            "stream_url": null,
            "comment": ""
          }
        },
        {
          "id": 3,
          "course_stu_id": 13,
          "course_team_id": 1,
          "is_leader": 0,
          "created_at": "2024-01-20 22:52:11",
          "updated_at": "2024-01-20 22:52:11",
          "deleted_at": null,
          "course_stu": {
            "id": 13,
            "course_id": 1,
            "user_id": 0,
            "nickname": "心心",
            "is_visitor": 1,
            "score": 0,
            "avatar_file_id": 0,
            "is_online": 1,
            "created_at": "2024-01-14 14:31:34",
            "updated_at": "2024-01-14 14:31:34",
            "deleted_at": null,
            "stream_url": null,
            "comment": ""
          }
        }
      ]
    },
    {
      "id": 2,
      "name": "B",
      "score": 0,
      "course_id": 1,
      "whiteboard_url": "url",
      "created_at": "2024-01-20 22:55:06",
      "updated_at": "2024-01-20 22:55:06",
      "deleted_at": null,
      "course_stu_teams": [
        {
          "id": 4,
          "course_stu_id": 10,
          "course_team_id": 2,
          "is_leader": 1,
          "created_at": "2024-01-20 22:55:06",
          "updated_at": "2024-01-20 22:55:06",
          "deleted_at": null,
          "course_stu": {
            "id": 10,
            "course_id": 1,
            "user_id": 0,
            "nickname": "心心",
            "is_visitor": 1,
            "score": 0,
            "avatar_file_id": 0,
            "is_online": 1,
            "created_at": "2024-01-13 17:25:22",
            "updated_at": "2024-01-13 17:25:22",
            "deleted_at": null,
            "stream_url": null,
            "comment": ""
          }
        },
        {
          "id": 5,
          "course_stu_id": 12,
          "course_team_id": 2,
          "is_leader": 0,
          "created_at": "2024-01-20 22:55:06",
          "updated_at": "2024-01-20 22:55:06",
          "deleted_at": null,
          "course_stu": {
            "id": 12,
            "course_id": 1,
            "user_id": 3,
            "nickname": "小明",
            "is_visitor": 0,
            "score": 0,
            "avatar_file_id": 0,
            "is_online": 1,
            "created_at": "2024-01-14 13:46:10",
            "updated_at": "2024-01-14 13:46:10",
            "deleted_at": null,
            "stream_url": null,
            "comment": ""
          }
        },
        {
          "id": 6,
          "course_stu_id": 5,
          "course_team_id": 2,
          "is_leader": 0,
          "created_at": "2024-01-20 22:55:06",
          "updated_at": "2024-01-20 22:55:06",
          "deleted_at": null,
          "course_stu": {
            "id": 5,
            "course_id": 1,
            "user_id": 0,
            "nickname": "小土",
            "is_visitor": 1,
            "score": 10,
            "avatar_file_id": 1,
            "is_online": 1,
            "created_at": "2023-12-30 13:06:05",
            "updated_at": "2024-01-19 11:17:15",
            "deleted_at": null,
            "stream_url": null,
            "comment": ""
          }
        }
      ]
    }
  ]
}
```

-失敗

#### 沒有權限

```json
{
  "result": false,
  "msg": ["You do not have permission to access this resource."]
}
```

### course_teams/my(GET)-學生取得自己課堂分組

#### Request

- Method: **GET**
- URL: `course_teams/my`
- Headers:
- Path-params:

| 名稱         | 類型 | 說明               | 範例                                | 是否必須 |
| :----------- | :--- | :----------------- | :---------------------------------- | :------- |
| Bearer Token |      | 有登入的學生必須要 |                                     | X        |
| token        |      | 訪客學生必須要     | 10-d401f35993b3f038d24c552b9b3c3a53 | X        |

#### Response

-成功

- Body:

```json
{
  {
  "result": true,
  "msg": [
    "Success"
  ],
  "data": [
    {
      "id": 1,
      "name": "A",
      "score": 0,
      "course_id": 1,
      "whiteboard_url": "url",
      "created_at": "2024-01-20 22:52:11",
      "updated_at": "2024-01-20 22:52:11",
      "deleted_at": null,
      "course_stu_teams": [
        {
          "id": 1,
          "course_stu_id": 1,
          "course_team_id": 1,
          "is_leader": 1,
          "created_at": "2024-01-20 22:52:11",
          "updated_at": "2024-01-20 22:52:11",
          "deleted_at": null,
          "course_stu": {
            "id": 1,
            "course_id": 1,
            "user_id": 0,
            "nickname": "小金",
            "is_visitor": 1,
            "score": 15,
            "avatar_file_id": 1,
            "is_online": 0,
            "created_at": "2023-12-29 09:24:06",
            "updated_at": "2024-01-20 11:45:09",
            "deleted_at": null,
            "stream_url": null,
            "comment": "表現優異"
          }
        },
        {
          "id": 2,
          "course_stu_id": 7,
          "course_team_id": 1,
          "is_leader": 0,
          "created_at": "2024-01-20 22:52:11",
          "updated_at": "2024-01-20 22:52:11",
          "deleted_at": null,
          "course_stu": {
            "id": 7,
            "course_id": 1,
            "user_id": 3,
            "nickname": "晶晶",
            "is_visitor": 0,
            "score": 0,
            "avatar_file_id": 0,
            "is_online": 1,
            "created_at": "2024-01-03 17:23:21",
            "updated_at": "2024-01-03 17:23:21",
            "deleted_at": null,
            "stream_url": null,
            "comment": ""
          }
        },
        {
          "id": 3,
          "course_stu_id": 13,
          "course_team_id": 1,
          "is_leader": 0,
          "created_at": "2024-01-20 22:52:11",
          "updated_at": "2024-01-20 22:52:11",
          "deleted_at": null,
          "course_stu": {
            "id": 13,
            "course_id": 1,
            "user_id": 0,
            "nickname": "心心",
            "is_visitor": 1,
            "score": 0,
            "avatar_file_id": 0,
            "is_online": 1,
            "created_at": "2024-01-14 14:31:34",
            "updated_at": "2024-01-14 14:31:34",
            "deleted_at": null,
            "stream_url": null,
            "comment": ""
          }
        }
      ]
    },
    {
      "id": 2,
      "name": "B",
      "score": 0,
      "course_id": 1,
      "whiteboard_url": "url",
      "created_at": "2024-01-20 22:55:06",
      "updated_at": "2024-01-20 22:55:06",
      "deleted_at": null,
      "course_stu_teams": [
        {
          "id": 4,
          "course_stu_id": 10,
          "course_team_id": 2,
          "is_leader": 1,
          "created_at": "2024-01-20 22:55:06",
          "updated_at": "2024-01-20 22:55:06",
          "deleted_at": null,
          "course_stu": {
            "id": 10,
            "course_id": 1,
            "user_id": 0,
            "nickname": "心心",
            "is_visitor": 1,
            "score": 0,
            "avatar_file_id": 0,
            "is_online": 1,
            "created_at": "2024-01-13 17:25:22",
            "updated_at": "2024-01-13 17:25:22",
            "deleted_at": null,
            "stream_url": null,
            "comment": ""
          }
        },
        {
          "id": 5,
          "course_stu_id": 12,
          "course_team_id": 2,
          "is_leader": 0,
          "created_at": "2024-01-20 22:55:06",
          "updated_at": "2024-01-20 22:55:06",
          "deleted_at": null,
          "course_stu": {
            "id": 12,
            "course_id": 1,
            "user_id": 3,
            "nickname": "小明",
            "is_visitor": 0,
            "score": 0,
            "avatar_file_id": 0,
            "is_online": 1,
            "created_at": "2024-01-14 13:46:10",
            "updated_at": "2024-01-14 13:46:10",
            "deleted_at": null,
            "stream_url": null,
            "comment": ""
          }
        },
        {
          "id": 6,
          "course_stu_id": 5,
          "course_team_id": 2,
          "is_leader": 0,
          "created_at": "2024-01-20 22:55:06",
          "updated_at": "2024-01-20 22:55:06",
          "deleted_at": null,
          "course_stu": {
            "id": 5,
            "course_id": 1,
            "user_id": 0,
            "nickname": "小土",
            "is_visitor": 1,
            "score": 10,
            "avatar_file_id": 1,
            "is_online": 1,
            "created_at": "2023-12-30 13:06:05",
            "updated_at": "2024-01-19 11:17:15",
            "deleted_at": null,
            "stream_url": null,
            "comment": ""
          }
        }
      ]
    }
  ]
}
}
```

-失敗

#### 沒有權限

```json
{
  "result": false,
  "msg": ["You do not have permission to access this resource."]
}
```

#### 尚未被分到組別 或 組別尚未建立

```json
{
  "result": false,
  "msg": ["You are not belong to any team now."]
}
```

### course_draw_lots/create(POST)-建立課堂抽籤

#### Request

- Method: **POST**
- URL: `course_draw_lots/create`
- Headers: Content-Type:multipart/form-data
- Path-params:

| 名稱         | 類型   | 說明                        | 範例 | 是否必須 |
| :----------- | :----- | :-------------------------- | :--- | :------- |
| course_id    | int    | 課堂 ID                     | 1    | O        |
| draw_type    | string | 值可為 stu(學生),team(分組) | stu  | O        |
| Bearer Token |        | 要為老師身分才可建立        |      | O        |

#### Response

-成功

- Body:

```json (stu)
{
  "result": true,
  "msg": ["Success"],
  "data": {
    "draw_type": "stu",
    "course_id": 1,
    "winner_id": 15,
    "participants": [
      {
        "id": 13,
        "course_id": 1,
        "user_id": 0,
        "nickname": "min",
        "is_visitor": 1,
        "score": 0,
        "avatar_file_id": 132,
        "is_online": 1,
        "created_at": "2024-01-14 14:31:34",
        "updated_at": "2024-02-24 12:00:14",
        "deleted_at": null,
        "stream_url": null,
        "comment": "",
        "avatar_file": {
          "id": 132,
          "uploader_id": 0,
          "uploader_type": "student",
          "file_type": "image",
          "course_id": 1,
          "drive_id": "/storage/NtjJqm055RMSkhZsA5I722tknId4beHEA1XNnGfz.png",
          "created_at": "2024-02-24 12:00:14",
          "updated_at": "2024-02-24 12:00:14",
          "deleted_at": null
        }
      },
      {
        "id": 15,
        "course_id": 1,
        "user_id": 0,
        "nickname": "心心",
        "is_visitor": 1,
        "score": 0,
        "avatar_file_id": 5,
        "is_online": 1,
        "created_at": "2024-01-16 22:36:33",
        "updated_at": "2024-01-16 22:36:33",
        "deleted_at": null,
        "stream_url": null,
        "comment": "",
        "avatar_file": {
          "id": 5,
          "uploader_id": 2,
          "uploader_type": "teacher",
          "file_type": "image",
          "course_id": 1,
          "drive_id": "/storage/BJ3pCI1q4AbgWNtpNfQLyU0nKg2rg6Nkd9z3sUM7.png",
          "created_at": "2024-01-05 16:23:54",
          "updated_at": "2024-01-05 16:23:54",
          "deleted_at": null
        }
      }
    ],
    "updated_at": "2024-02-24 12:33:41",
    "created_at": "2024-02-24 12:33:41",
    "id": 32
  }
}
```

```json (team)
{
  "result": true,
  "msg": ["Success"],
  "data": {
    "draw_type": "team",
    "course_id": 1,
    "winner_id": 48,
    "participants": [
      {
        "id": 47,
        "name": "A",
        "score": 0,
        "course_id": 1,
        "whiteboard_url": "url",
        "created_at": "2024-01-23 17:41:23",
        "updated_at": "2024-01-23 17:41:23",
        "deleted_at": null
      },
      {
        "id": 48,
        "name": "B",
        "score": 0,
        "course_id": 1,
        "whiteboard_url": "url",
        "created_at": "2024-01-23 17:41:23",
        "updated_at": "2024-01-23 17:41:23",
        "deleted_at": null
      },
      {
        "id": 49,
        "name": "C",
        "score": 0,
        "course_id": 1,
        "whiteboard_url": "url",
        "created_at": "2024-01-23 17:41:23",
        "updated_at": "2024-01-23 17:41:23",
        "deleted_at": null
      }
    ],
    "updated_at": "2024-01-23 17:57:23",
    "created_at": "2024-01-23 17:57:23",
    "id": 30
  }
}
```

-失敗

#### 沒有權限(不是老師)

- Status: 403 Forbidden
- Body:

```json
{
  "result": false,
  "msg": ["You do not have permission to access this resource."]
}
```

#### 課堂沒有學生/組別

- Body:

```json
{
  "result": false,
  "msg": ["No participants."]
}
```

#### MQTT

```json
{
  "course_data": "略",
  "status": "task",
  "api": "course_draw_lots/{id}",
  "method": "get",
  "course_stu_ids": []
}
```

### course_draw_lots/{id}(GET)-取得課堂抽籤結果

#### Request

- Method: **GET**
- URL: `course_draw_lots/{id}`
- Headers:
- Path-params:

| 名稱         | 類型 | 說明                    | 範例                                | 是否必須 |
| :----------- | :--- | :---------------------- | :---------------------------------- | :------- |
| id           | int  | 抽籤 ID                 | 1                                   | O        |
| Bearer Token |      | 有登入的學生/老師必須要 |                                     | X        |
| token        |      | 訪客學生必須要          | 10-d401f35993b3f038d24c552b9b3c3a53 | X        |

#### Response

-成功

- Body:

```json (老師)
{
  "result": true,
  "msg": ["Success"],
  "data": {
    "id": 41,
    "course_id": 1,
    "draw_type": "stu",
    "winner_id": 25,
    "participants": [
      {
        "id": 4,
        "course_id": 1,
        "user_id": 0,
        "nickname": "小火",
        "is_visitor": 1,
        "score": 0,
        "avatar_file_id": 1,
        "is_online": 1,
        "created_at": "2023-12-30 11:39:56",
        "updated_at": "2024-02-23 11:47:16",
        "deleted_at": null,
        "stream_url": null,
        "comment": "",
        "avatar_file": {
          "id": 1,
          "uploader_id": 0,
          "uploader_type": "student",
          "file_type": "image",
          "course_id": 1,
          "drive_id": "/storage/GOMQXKw0NRF5CAq3HBOk7fx1cntuk1sxrirZDoCV.png",
          "created_at": "2023-12-30 11:32:58",
          "updated_at": "2023-12-30 11:32:58",
          "deleted_at": null
        }
      },
      {
        "id": 5,
        "course_id": 1,
        "user_id": 0,
        "nickname": "小土",
        "is_visitor": 1,
        "score": 0,
        "avatar_file_id": 1,
        "is_online": 1,
        "created_at": "2023-12-30 13:06:05",
        "updated_at": "2024-02-23 11:47:16",
        "deleted_at": null,
        "stream_url": null,
        "comment": "",
        "avatar_file": {
          "id": 1,
          "uploader_id": 0,
          "uploader_type": "student",
          "file_type": "image",
          "course_id": 1,
          "drive_id": "/storage/GOMQXKw0NRF5CAq3HBOk7fx1cntuk1sxrirZDoCV.png",
          "created_at": "2023-12-30 11:32:58",
          "updated_at": "2023-12-30 11:32:58",
          "deleted_at": null
        }
      }
    ],
    "created_at": "2024-03-18 21:14:03",
    "updated_at": "2024-03-18 21:14:03",
    "deleted_at": null,
    "course": {
      "id": 1,
      "user_id": 2,
      "class_name": "一年一班",
      "subject": "數學",
      "code": "yMdlXBrpo9",
      "is_open": 1,
      "status": "draw",
      "created_at": "2023-12-28 11:15:04",
      "updated_at": "2024-03-18 21:30:04",
      "deleted_at": null,
      "status_id": 61,
      "qrcode_svg": "<?xml version=\"1.0\" encoding=\"UTF-8\"?>\n<svg xmlns=\"http://www.w3.org/2000/svg\" version=\"1.1\" width=\"100\" height=\"100\" viewBox=\"0 0 100 100\"><rect x=\"0\" y=\"0\" width=\"100\" height=\"100\" fill=\"#ffffff\"/><g transform=\"scale(4.762)\"><g transform=\"translate(0,0)\"><path fill-rule=\"evenodd\" d=\"M8 0L8 1L9 1L9 2L8 2L8 5L11 5L11 4L12 4L12 3L13 3L13 0L12 0L12 3L11 3L11 2L10 2L10 0ZM9 2L9 4L11 4L11 3L10 3L10 2ZM8 6L8 7L9 7L9 8L8 8L8 9L9 9L9 10L6 10L6 9L7 9L7 8L6 8L6 9L4 9L4 8L0 8L0 9L1 9L1 10L0 10L0 11L3 11L3 12L2 12L2 13L8 13L8 14L9 14L9 16L10 16L10 17L8 17L8 21L9 21L9 19L10 19L10 17L12 17L12 16L13 16L13 19L12 19L12 18L11 18L11 21L14 21L14 20L15 20L15 19L14 19L14 18L15 18L15 17L14 17L14 16L13 16L13 15L11 15L11 13L12 13L12 12L13 12L13 9L14 9L14 8L13 8L13 9L12 9L12 12L10 12L10 14L9 14L9 12L8 12L8 11L9 11L9 10L10 10L10 9L11 9L11 6L10 6L10 7L9 7L9 6ZM12 6L12 7L13 7L13 6ZM9 8L9 9L10 9L10 8ZM16 8L16 10L14 10L14 11L16 11L16 10L18 10L18 9L19 9L19 8ZM20 8L20 9L21 9L21 8ZM2 9L2 10L3 10L3 11L4 11L4 9ZM19 10L19 11L21 11L21 10ZM6 11L6 12L7 12L7 11ZM17 11L17 12L18 12L18 11ZM0 12L0 13L1 13L1 12ZM14 12L14 13L13 13L13 14L14 14L14 15L15 15L15 16L17 16L17 17L16 17L16 18L18 18L18 19L19 19L19 18L20 18L20 17L19 17L19 15L17 15L17 13L16 13L16 12ZM20 12L20 13L19 13L19 14L20 14L20 13L21 13L21 12ZM14 13L14 14L15 14L15 13ZM20 15L20 16L21 16L21 15ZM13 19L13 20L14 20L14 19ZM20 19L20 20L21 20L21 19ZM17 20L17 21L18 21L18 20ZM0 0L0 7L7 7L7 0ZM1 1L1 6L6 6L6 1ZM2 2L2 5L5 5L5 2ZM14 0L14 7L21 7L21 0ZM15 1L15 6L20 6L20 1ZM16 2L16 5L19 5L19 2ZM0 14L0 21L7 21L7 14ZM1 15L1 20L6 20L6 15ZM2 16L2 19L5 19L5 16Z\" fill=\"#000000\"/></g></g></svg>\n"
    }
  }
}
```

```json (學生)
{
  "result": true,
  "msg": ["Success"],
  "data": {
    "is_winner": true
  }
}
```

-失敗

#### 沒有權限

```json
{
  "result": false,
  "msg": ["You do not have permission to access this resource."]
}
```

### courses/{id}/course_draw_lots(GET)-取得課堂所有抽籤結果

#### Request

- Method: **GET**
- URL: `courses/{id}/course_draw_lots`
- Headers:
- Path-params:

| 名稱         | 類型 | 說明           | 範例 | 是否必須 |
| :----------- | :--- | :------------- | :--- | :------- |
| id           | int  | 課堂 ID        | 1    | O        |
| Bearer Token |      | 只有老師可以用 |      | O        |

#### Response

-成功

- Body:

```json (老師)
{
  "result": true,
  "msg": ["Success"],
  "data": [
    {
      "id": 41,
      "course_id": 1,
      "draw_type": "stu",
      "winner_id": 4,
      "participants": [
        {
          "id": 4,
          "course_id": 1,
          "user_id": 0,
          "nickname": "小火",
          "is_visitor": 1,
          "score": 0,
          "avatar_file_id": 1,
          "is_online": 1,
          "created_at": "2023-12-30 11:39:56",
          "updated_at": "2024-02-23 11:47:16",
          "deleted_at": null,
          "stream_url": null,
          "comment": "",
          "avatar_file": {
            "id": 1,
            "uploader_id": 0,
            "uploader_type": "student",
            "file_type": "image",
            "course_id": 1,
            "drive_id": "/storage/GOMQXKw0NRF5CAq3HBOk7fx1cntuk1sxrirZDoCV.png",
            "created_at": "2023-12-30 11:32:58",
            "updated_at": "2023-12-30 11:32:58",
            "deleted_at": null
          }
        },
        {
          "id": 5,
          "course_id": 1,
          "user_id": 0,
          "nickname": "小土",
          "is_visitor": 1,
          "score": 0,
          "avatar_file_id": 1,
          "is_online": 1,
          "created_at": "2023-12-30 13:06:05",
          "updated_at": "2024-02-23 11:47:16",
          "deleted_at": null,
          "stream_url": null,
          "comment": "",
          "avatar_file": {
            "id": 1,
            "uploader_id": 0,
            "uploader_type": "student",
            "file_type": "image",
            "course_id": 1,
            "drive_id": "/storage/GOMQXKw0NRF5CAq3HBOk7fx1cntuk1sxrirZDoCV.png",
            "created_at": "2023-12-30 11:32:58",
            "updated_at": "2023-12-30 11:32:58",
            "deleted_at": null
          }
        }
      ],
      "created_at": "2024-03-18 21:14:03",
      "updated_at": "2024-03-18 21:14:03",
      "deleted_at": null
    },
    {
      "id": 42,
      "course_id": 1,
      "draw_type": "stu",
      "winner_id": 5,
      "participants": [
        {
          "id": 4,
          "course_id": 1,
          "user_id": 0,
          "nickname": "小火",
          "is_visitor": 1,
          "score": 0,
          "avatar_file_id": 1,
          "is_online": 1,
          "created_at": "2023-12-30 11:39:56",
          "updated_at": "2024-02-23 11:47:16",
          "deleted_at": null,
          "stream_url": null,
          "comment": "",
          "avatar_file": {
            "id": 1,
            "uploader_id": 0,
            "uploader_type": "student",
            "file_type": "image",
            "course_id": 1,
            "drive_id": "/storage/GOMQXKw0NRF5CAq3HBOk7fx1cntuk1sxrirZDoCV.png",
            "created_at": "2023-12-30 11:32:58",
            "updated_at": "2023-12-30 11:32:58",
            "deleted_at": null
          }
        },
        {
          "id": 5,
          "course_id": 1,
          "user_id": 0,
          "nickname": "小土",
          "is_visitor": 1,
          "score": 0,
          "avatar_file_id": 1,
          "is_online": 1,
          "created_at": "2023-12-30 13:06:05",
          "updated_at": "2024-02-23 11:47:16",
          "deleted_at": null,
          "stream_url": null,
          "comment": "",
          "avatar_file": {
            "id": 1,
            "uploader_id": 0,
            "uploader_type": "student",
            "file_type": "image",
            "course_id": 1,
            "drive_id": "/storage/GOMQXKw0NRF5CAq3HBOk7fx1cntuk1sxrirZDoCV.png",
            "created_at": "2023-12-30 11:32:58",
            "updated_at": "2023-12-30 11:32:58",
            "deleted_at": null
          }
        }
      ],
      "created_at": "2024-03-18 21:15:10",
      "updated_at": "2024-03-18 21:15:10",
      "deleted_at": null
    }
  ]
}
```

-失敗

#### 沒有權限

```json
{
  "result": false,
  "msg": ["You do not have permission to access this resource."]
}
```

### 課堂任務-MQTT/取得學生個人化狀態說明

#### 教師:課堂任務發送 MQTT

| 時機                                                    | status         | api                                        | method | 課堂任務 is_active |
| :------------------------------------------------------ | :------------- | :----------------------------------------- | :----- | :----------------- |
| 老師執行 API `course_tasks/create` 成功後               | task           | `course_tasks/{id}/actions/get_stu_status` | get    | 1                  |
| 老師執行 API `course_tasks/{id}/actions/close` 成功後   | task_closed    |                                            |        | 0                  |
| 老師執行 API `course_tasks/{id}/actions/correct` 成功後 | task_corrected | `course_tasks/{id}/actions/get_correct`    | get    | 1                  |

#### 學生:課堂任務學生取得個人化狀態

| 時機說明             | status         | api                                     | method | 課堂任務 is_active |
| :------------------- | :------------- | :-------------------------------------- | :----- | :----------------- |
| 任務未開始/已結束    | task_closed    |                                         |        | 0                  |
| 學生還沒回答         | task_answering | `course_tasks/{id}/actions/answer `     | post   | 1                  |
| 學生已回答           | task_answered  |                                         |        | 1                  |
| 任務已被老師批改完成 | task_corrected | `course_tasks/{id}/actions/get_correct` | get    | 1                  |

### course_tasks/create(POST)-建立課堂任務

#### Request

- Method: **POST**
- URL: `course_tasks/create`
- Headers: Content-Type:multipart/form-data
- Path-params:

| 名稱         | 類型   | 說明                                             | 範例   | 是否必須 |
| :----------- | :----- | :----------------------------------------------- | :----- | :------- |
| course_id    | int    | 課堂 ID                                          | 1      | O        |
| task_type    | string | 值可為 record(錄音),file(檔案),audiovisual(影音) | record | O        |
| Bearer Token |        | 要為老師身分才可建立                             |        | O        |

#### Response

-成功

- Body:

```json
{
  "result": true,
  "msg": ["Success"],
  "data": {
    "id": 8
  }
}
```

-失敗

#### 沒有權限(不是老師)

- Status: 403 Forbidden
- Body:

```json
{
  "result": false,
  "msg": ["You do not have permission to access this resource."]
}
```

#### MQTT

```json
{
  "course_data": "略",
  "status": "task",
  "api": "course_tasks/{id}/actions/get_stu_status",
  "method": "get",
  "course_stu_ids": []
}
```

### course_tasks/{id}(GET)-取得課堂任務

#### Request

- Method: **GET**
- URL: `course_tasks/{id}`
- Headers:
- Path-params:

| 名稱         | 類型 | 說明                    | 範例                                | 是否必須 |
| :----------- | :--- | :---------------------- | :---------------------------------- | :------- |
| id           | int  | 課堂任務 ID             | 1                                   | O        |
| Bearer Token |      | 有登入的學生/老師必須要 |                                     | X        |
| token        |      | 訪客學生必須要          | 10-d401f35993b3f038d24c552b9b3c3a53 | X        |

#### Response

- param:

| 名稱           | 類型    | 說明         | 範例 |
| :------------- | :------ | :----------- | :--- |
| correct_answer | string  | 正確答案     | 1    |
| is_active      | boolean | 課堂搶答狀態 | 1    |

- is_active 說明參考[課堂任務-MQTT/取得學生個人化狀態說明](#課堂搶答-MQTT/取得學生個人化狀態說明) 課堂搶答 is_active 欄位

-成功

- Body:

```json
{
  "result": true,
  "msg": ["Success"],
  "data": {
    "course_task": {
      "id": 7,
      "course_id": 1,
      "task_type": "record",
      "is_active": 1,
      "created_at": "2024-02-03 10:46:56",
      "updated_at": "2024-02-03 10:46:56",
      "deleted_at": null,
      "course": {
        "id": 1,
        "user_id": 2,
        "class_name": "一年一班",
        "subject": "數學",
        "code": "yMdlXBrpo9",
        "is_open": 1,
        "status": "task",
        "created_at": "2023-12-28 11:15:04",
        "updated_at": "2024-02-03 15:28:56",
        "deleted_at": null,
        "status_id": 8,
        "qrcode_svg": "<?xml version=\"1.0\" encoding=\"UTF-8\"?>\n<svg xmlns=\"http://www.w3.org/2000/svg\" version=\"1.1\" width=\"100\" height=\"100\" viewBox=\"0 0 100 100\"><rect x=\"0\" y=\"0\" width=\"100\" height=\"100\" fill=\"#ffffff\"/><g transform=\"scale(4.762)\"><g transform=\"translate(0,0)\"><path fill-rule=\"evenodd\" d=\"M8 0L8 1L9 1L9 2L8 2L8 5L11 5L11 4L12 4L12 3L13 3L13 0L12 0L12 3L11 3L11 2L10 2L10 0ZM9 2L9 4L11 4L11 3L10 3L10 2ZM8 6L8 7L9 7L9 8L8 8L8 9L9 9L9 10L6 10L6 9L7 9L7 8L6 8L6 9L4 9L4 8L0 8L0 9L1 9L1 10L0 10L0 11L3 11L3 12L2 12L2 13L8 13L8 14L9 14L9 16L10 16L10 17L8 17L8 21L9 21L9 19L10 19L10 17L12 17L12 16L13 16L13 19L12 19L12 18L11 18L11 21L14 21L14 20L15 20L15 19L14 19L14 18L15 18L15 17L14 17L14 16L13 16L13 15L11 15L11 13L12 13L12 12L13 12L13 9L14 9L14 8L13 8L13 9L12 9L12 12L10 12L10 14L9 14L9 12L8 12L8 11L9 11L9 10L10 10L10 9L11 9L11 6L10 6L10 7L9 7L9 6ZM12 6L12 7L13 7L13 6ZM9 8L9 9L10 9L10 8ZM16 8L16 10L14 10L14 11L16 11L16 10L18 10L18 9L19 9L19 8ZM20 8L20 9L21 9L21 8ZM2 9L2 10L3 10L3 11L4 11L4 9ZM19 10L19 11L21 11L21 10ZM6 11L6 12L7 12L7 11ZM17 11L17 12L18 12L18 11ZM0 12L0 13L1 13L1 12ZM14 12L14 13L13 13L13 14L14 14L14 15L15 15L15 16L17 16L17 17L16 17L16 18L18 18L18 19L19 19L19 18L20 18L20 17L19 17L19 15L17 15L17 13L16 13L16 12ZM20 12L20 13L19 13L19 14L20 14L20 13L21 13L21 12ZM14 13L14 14L15 14L15 13ZM20 15L20 16L21 16L21 15ZM13 19L13 20L14 20L14 19ZM20 19L20 20L21 20L21 19ZM17 20L17 21L18 21L18 20ZM0 0L0 7L7 7L7 0ZM1 1L1 6L6 6L6 1ZM2 2L2 5L5 5L5 2ZM14 0L14 7L21 7L21 0ZM15 1L15 6L20 6L20 1ZM16 2L16 5L19 5L19 2ZM0 14L0 21L7 21L7 14ZM1 15L1 20L6 20L6 15ZM2 16L2 19L5 19L5 16Z\" fill=\"#000000\"/></g></g></svg>\n"
      }
    }
  }
}
```

-失敗

#### 沒有權限

```json
{
  "result": false,
  "msg": ["You do not have permission to access this resource."]
}
```

### course_tasks/{id}/actions/answer(POST)-學生回答課堂任務

#### Request

- Method: **POST**
- URL: `course_tasks/{id}/actions/answer`
- Headers: Content-Type:multipart/form-data
- Path-params:

| 名稱         | 類型 | 說明                            | 範例                                | 是否必須 |
| :----------- | :--- | :------------------------------ | :---------------------------------- | :------- |
| answer_file  | file | 回答課堂任務圖片/音訊/影片/檔案 |                                     | O        |
| length       | int  | 回答若為音訊, 須回傳秒數        | 120                                 | X        |
| Bearer Token |      | 有登入的學生必須要              |                                     | X        |
| token        |      | 訪客學生必須要                  | 10-d401f35993b3f038d24c552b9b3c3a53 | X        |

#### Response

-成功

- Body:

```json
{
  "result": true,
  "msg": ["Success"],
  "data": []
}
```

-失敗

#### 沒有權限

- Status: 403 Forbidden
- Body:

```json
{
  "result": false,
  "msg": ["You do not have permission to access this resource."]
}
```

#### 已經回答過任務

```json
{
  "result": false,
  "msg": ["Answer already exists."]
}
```

#### 任務已經結束

```json
{
  "result": false,
  "msg": ["Task is not active."]
}
```

### course_tasks/{id}/actions/get_answer?course_stu_id={course_stu_id}(GET)-老師取得學生任務答案

#### Request

- Method: **GET**
- URL: `course_tasks/{id}/actions/get_answer?course_stu_id={course_stu_id}`
- Headers:
- Path-params:

| 名稱          | 類型 | 說明                                 | 範例 | 是否必須 |
| :------------ | :--- | :----------------------------------- | :--- | :------- |
| id            | int  | 課堂任務 ID                          | 1    | O        |
| course_stu_id | int  | 課堂學生 ID (沒給就是取得全班的回答) | 1    | X        |
| Bearer Token  |      |                                      |      | O        |

#### Response

-成功

- Body:

(answer_file 為 null 表示還沒交答案)

```json (全班)
{
  "result": true,
  "msg": ["Success"],
  "data": [
    {
      "id": 10,
      "course_task_id": 7,
      "course_stu_id": 4,
      "answer_file_id": null,
      "length": null,
      "correct_file_id": null,
      "file_type": "record",
      "created_at": "2024-02-03 10:46:56",
      "updated_at": "2024-02-03 10:46:56",
      "deleted_at": null,
      "answer_file": null
    },
    {
      "id": 11,
      "course_task_id": 7,
      "course_stu_id": 5,
      "answer_file_id": null,
      "length": null,
      "correct_file_id": null,
      "file_type": "record",
      "created_at": "2024-02-03 10:46:56",
      "updated_at": "2024-02-03 10:46:56",
      "deleted_at": null,
      "answer_file": null
    },
    {
      "id": 12,
      "course_task_id": 7,
      "course_stu_id": 7,
      "answer_file_id": null,
      "length": null,
      "correct_file_id": null,
      "file_type": "record",
      "created_at": "2024-02-03 10:46:56",
      "updated_at": "2024-02-03 10:46:56",
      "deleted_at": null,
      "answer_file": null
    },
    {
      "id": 13,
      "course_task_id": 7,
      "course_stu_id": 9,
      "answer_file_id": null,
      "length": null,
      "correct_file_id": null,
      "file_type": "record",
      "created_at": "2024-02-03 10:46:56",
      "updated_at": "2024-02-03 10:46:56",
      "deleted_at": null,
      "answer_file": null
    },
    {
      "id": 14,
      "course_task_id": 7,
      "course_stu_id": 10,
      "answer_file_id": null,
      "length": null,
      "correct_file_id": null,
      "file_type": "record",
      "created_at": "2024-02-03 10:46:56",
      "updated_at": "2024-02-03 10:46:56",
      "deleted_at": null,
      "answer_file": null
    },
    {
      "id": 15,
      "course_task_id": 7,
      "course_stu_id": 11,
      "answer_file_id": null,
      "length": null,
      "correct_file_id": null,
      "file_type": "record",
      "created_at": "2024-02-03 10:46:56",
      "updated_at": "2024-02-03 10:46:56",
      "deleted_at": null,
      "answer_file": null
    },
    {
      "id": 16,
      "course_task_id": 7,
      "course_stu_id": 12,
      "answer_file_id": 50,
      "length": 10,
      "correct_file_id": null,
      "file_type": "record",
      "created_at": "2024-02-03 10:46:56",
      "updated_at": "2024-02-03 10:55:40",
      "deleted_at": null,
      "answer_file": {
        "id": 50,
        "uploader_id": 3,
        "uploader_type": "student",
        "file_type": "record",
        "course_id": 1,
        "drive_id": "0z7KK006FhogG2OHnUEA95VhjRf7XGdoA2Y3U7Cm.m4a",
        "created_at": "2024-02-03 10:55:40",
        "updated_at": "2024-02-03 10:55:40",
        "deleted_at": null
      }
    },
    {
      "id": 17,
      "course_task_id": 7,
      "course_stu_id": 13,
      "answer_file_id": null,
      "length": null,
      "correct_file_id": null,
      "file_type": "record",
      "created_at": "2024-02-03 10:46:56",
      "updated_at": "2024-02-03 10:46:56",
      "deleted_at": null,
      "answer_file": null
    },
    {
      "id": 18,
      "course_task_id": 7,
      "course_stu_id": 15,
      "answer_file_id": null,
      "length": null,
      "correct_file_id": null,
      "file_type": "record",
      "created_at": "2024-02-03 10:46:56",
      "updated_at": "2024-02-03 10:46:56",
      "deleted_at": null,
      "answer_file": null
    }
  ]
}
```

```json (單一個人)
{
  "result": true,
  "msg": ["Success"],
  "data": {
    "id": 61,
    "uploader_id": 0,
    "uploader_type": "student",
    "file_type": "audiovisual",
    "course_id": 1,
    "drive_id": "mBk8iaasTteAYrzrnQFNp5sL0YDB1XsMSpTlNp2u.jpg",
    "created_at": "2024-02-03 17:45:48",
    "updated_at": "2024-02-03 17:45:48",
    "deleted_at": null
  }
}
```

-失敗

#### 課堂快問快答不存在

- Status: 404 Not Found
- Body

```json
{
  "result": false,
  "msg": ["CourseQuiz with id 13 not found."]
}
```

#### 不是該堂課的老師

- Body

```json
{
  "result": false,
  "msg": ["You do not have permission to access this resource."]
}
```

### course_tasks/{id}/actions/correct(POST)-老師批閱學生任務答案

#### Request

- Method: **POST**
- URL: `course_tasks/{id}/actions/correct`
- Headers: Content-Type:multipart/form-data
- Path-params:

| 名稱          | 類型 | 說明        | 範例 | 是否必須 |
| :------------ | :--- | :---------- | :--- | :------- |
| id            | int  | 課堂任務 ID | 1    | O        |
| correct_file  | file | 批閱圖片    |      | O        |
| course_stu_id | int  | 課堂學生 ID | 1    | O        |
| Bearer Token  |      |             |      | O        |

**_ 只有影音任務才可批閱 _**

#### Response

-成功

- Body:

```json
{
  "result": true,
  "msg": ["Success"],
  "data": []
}
```

-失敗

#### 沒有權限

- Status: 403 Forbidden
- Body:

```json
{
  "result": false,
  "msg": ["You do not have permission to access this resource."]
}
```

#### 不是影音任務

```json
{
  "result": false,
  "msg": ["Task is not a audiovisual task."]
}
```

#### MQTT

```json
{
  "course_data": "略",
  "status": "task_corrected",
  "api": "course_tasks/{id}/actions/get_correct",
  "method": "get",
  "parameter": "{course_stu_id}"
}
```

### course_tasks/{id}/actions/get_correct?token={token}(GET)-學生取得老師任務批閱結果

#### Request

- Method: **GET**
- URL: `course_tasks/{id}/actions/get_correct?token={token}`
- Headers:
- Path-params:

| 名稱         | 類型 | 說明               | 範例                                | 是否必須 |
| :----------- | :--- | :----------------- | :---------------------------------- | :------- |
| id           | int  | 課堂任務 ID        | 1                                   | O        |
| Bearer Token |      | 有登入的學生必須要 |                                     | X        |
| token        |      | 訪客學生必須要     | 10-d401f35993b3f038d24c552b9b3c3a53 | X        |

**_ 只有影音任務才可取得批閱結果 _**

#### Response

-成功

- Body:

```json
{
  "result": true,
  "msg": ["Success"],
  "data": {
    "id": 62,
    "uploader_id": 2,
    "uploader_type": "teacher",
    "file_type": "image",
    "course_id": 1,
    "drive_id": "02HKGx8JVx8zUnWfB7tDalx0wkhyayue9aNKVnVe.jpg",
    "created_at": "2024-02-03 17:48:38",
    "updated_at": "2024-02-03 17:48:38",
    "deleted_at": null
  }
}
```

-失敗

#### 課堂任務不存在

- Status: 404 Not Found
- Body

```json
{
  "result": false,
  "msg": ["CourseQuiz with id 13 not found."]
}
```

#### 批閱結果不存在

```json
{
  "result": false,
  "msg": ["Correct file not exists."]
}
```

### course_tasks/{id}/actions/close(POST)-老師結束任務

#### Request

- Method: **POST**
- URL: `course_tasks/{id}/actions/close`
- Headers: Content-Type:multipart/form-data
- Path-params:

| 名稱         | 類型 | 說明        | 範例 | 是否必須 |
| :----------- | :--- | :---------- | :--- | :------- |
| id           | int  | 課堂任務 ID | 1    | O        |
| Bearer Token |      |             |      | O        |

#### Response

-成功

- Body:

```json
{
  "result": true,
  "msg": ["Success"],
  "data": []
}
```

-失敗

#### 沒有權限

- Status: 403 Forbidden
- Body:

```json
{
  "result": false,
  "msg": ["You do not have permission to access this resource."]
}
```

#### MQTT

```json
{
  "course_data": "略",
  "status": "task_closed",
  "api": "",
  "method": "",
  "course_stu_ids": []
}
```

### course_tasks/{id}/actions/get_stu_status(GET)-取得學生個人課堂任務狀態

#### Request

- Method: **GET**
- URL: `course_tasks/{id}/actions/get_stu_status`
- Headers:
- Path-params:

| 名稱         | 類型 | 說明                    | 範例                                | 是否必須 |
| :----------- | :--- | :---------------------- | :---------------------------------- | :------- |
| id           | int  | 課堂任務 ID             | 1                                   | O        |
| Bearer Token |      | 有登入的學生/老師必須要 |                                     | X        |
| token        |      | 訪客學生必須要          | 10-d401f35993b3f038d24c552b9b3c3a53 | X        |

- return-params:

| 名稱   | 類型  | 說明                                        | 範例        |
| :----- | :---- | :------------------------------------------ | :---------- |
| data   | int   | 如 api 是 get 類型，會先傳該 api 回覆的資料 |             |
| status | int   | 除了狀態包含 MQTT 發送的狀態之外            | task_closed |
| api    | int   | api 路徑                                    |             |
| method | array | api 方法                                    |             |

- [回傳內容說明參考](#課堂任務學生取得個人化狀態)

#### Response

-成功

- Body:

```json
{
  "result": true,
  "msg": ["Success"],
  "data": [],
  "status": "quiz_time_up",
  "api": "",
  "method": "",
  "parameter": []
}
```

-失敗

#### 沒有權限

```json
{
  "result": false,
  "msg": ["You do not have permission to access this resource."]
}
```

### 課堂搶答-MQTT/取得學生個人化狀態說明

#### 教師:課堂搶答發送 MQTT

| 時機                                                         | status       | api                                      | method | 課堂搶答 status |
| :----------------------------------------------------------- | :----------- | :--------------------------------------- | :----- | :-------------- |
| 老師執行 API `course_qas/create` 成功後                      | qa           | `course_qas/{id}/actions/get_stu_status` | get    | closed          |
| 老師執行 API `course_qas/{id}/actions/run` 成功後            | qa_answering | `course_qas/{id}/actions/answer`         | post   | running         |
| 老師執行 API `course_qas/{id}/actions/stop` 成功後           | qa_stopped   |                                          |        | stopped         |
| 老師執行 API `course_qas/{id}/actions/time_up` 成功後        | qa_time_up   |                                          |        | time_up         |
| 老師執行 API `course_qas/{id}/actions/publish_answer` 成功後 | qa_complete  | `course_qas/{id}/actions/get_result`     | get    | complete        |

#### 學生:課堂搶答學生取得個人化狀態

| 時機說明                                | status              | api                                  | method | 課堂搶答 status |
| :-------------------------------------- | :------------------ | :----------------------------------- | :----- | :-------------- |
| 搶答未開始                              | qa_closed           |                                      |        | closed          |
| (加分)還沒人搶答成功/(競賽)學生還沒回答 | qa_answering        | `course_qas/{id}/actions/answer `    | post   | running         |
| (競賽)學生已回答                        | qa_answered         |                                      |        | running         |
| (加分)已有人成功搶答                    | qa_answered_success | `course_qas/{id}/actions/get_result` | get    | answered        |
| 搶答被中止                              | qa_stopped          |                                      |        | stopped         |
| 搶答時間到                              | qa_time_up          |                                      |        | time_up         |
| 搶答已完成                              | qa_complete         | `course_qas/{id}/actions/get_result` | get    | complete        |

### course_qas/create(POST)-建立課堂搶答

#### Request

- Method: **POST**
- URL: `course_qas/create`
- Headers: Content-Type:multipart/form-data
- Path-params:

| 名稱         | 類型   | 說明                                                   | 範例  | 是否必須 |
| :----------- | :----- | :----------------------------------------------------- | :---- | :------- |
| course_id    | int    | 課堂 ID                                                | 1     | O        |
| qa_type      | string | 值可為 score(加分搶答),competition(競賽搶答)           | score | O        |
| time_period  | int    | 搶答時間(秒數), qa_type 為 competition(競賽搶答)才需要 | 120   | X        |
| target_type  | string | 搶答對象類型(stu/team)                                 | stu   | O        |
| Bearer Token |        | 要為老師身分才可建立                                   |       | O        |

- 狀態說明
  課堂搶答執行此 API 成功後狀態會更新為 closed

#### Response

-成功

- Body:

```json
{
  "result": true,
  "msg": ["Success"],
  "data": {
    "id": 8
  }
}
```

-失敗

#### 沒有權限(不是老師)

- Status: 403 Forbidden
- Body:

```json
{
  "result": false,
  "msg": ["You do not have permission to access this resource."]
}
```

#### MQTT

```json
{
  "course_data": "略",
  "status": "qa",
  "api": "course_qas/7/actions/get_stu_status",
  "method": "get",
  "course_stu_ids": []
}
```

### course_qas/{id}(GET)-取得課堂搶答

#### Request

- Method: **GET**
- URL: `course_qas/{id}`
- Headers:
- Path-params:

| 名稱         | 類型 | 說明                    | 範例                                | 是否必須 |
| :----------- | :--- | :---------------------- | :---------------------------------- | :------- |
| id           | int  | 課堂搶答 ID             | 1                                   | O        |
| Bearer Token |      | 有登入的學生/老師必須要 |                                     | X        |
| token        |      | 訪客學生必須要          | 10-d401f35993b3f038d24c552b9b3c3a53 | X        |

#### Response

- param:

| 名稱           | 類型   | 說明         | 範例    |
| :------------- | :----- | :----------- | :------ |
| correct_answer | string | 正確答案     | 1       |
| status         | string | 課堂搶答狀態 | running |

- status 說明參考[課堂搶答-MQTT/取得學生個人化狀態說明](#課堂搶答-MQTT/取得學生個人化狀態說明) 課堂搶答 status 欄位

-成功

- Body:

```json
{
  "result": true,
  "msg": ["Success"],
  "data": {
    "id": 2,
    "course_id": 1,
    "correct_answer": null,
    "qa_type": "score",
    "time_period": null,
    "created_at": "2024-02-04 13:01:16",
    "updated_at": "2024-02-04 13:01:16",
    "deleted_at": null,
    "status": "closed",
    "course": {
      "id": 1,
      "user_id": 2,
      "class_name": "一年一班",
      "subject": "數學",
      "code": "yMdlXBrpo9",
      "is_open": 1,
      "status": "qa",
      "created_at": "2023-12-28 11:15:04",
      "updated_at": "2024-02-04 13:01:52",
      "deleted_at": null,
      "status_id": 3,
      "qrcode_svg": "<?xml version=\"1.0\" encoding=\"UTF-8\"?>\n<svg xmlns=\"http://www.w3.org/2000/svg\" version=\"1.1\" width=\"100\" height=\"100\" viewBox=\"0 0 100 100\"><rect x=\"0\" y=\"0\" width=\"100\" height=\"100\" fill=\"#ffffff\"/><g transform=\"scale(4.762)\"><g transform=\"translate(0,0)\"><path fill-rule=\"evenodd\" d=\"M8 0L8 1L9 1L9 2L8 2L8 5L11 5L11 4L12 4L12 3L13 3L13 0L12 0L12 3L11 3L11 2L10 2L10 0ZM9 2L9 4L11 4L11 3L10 3L10 2ZM8 6L8 7L9 7L9 8L8 8L8 9L9 9L9 10L6 10L6 9L7 9L7 8L6 8L6 9L4 9L4 8L0 8L0 9L1 9L1 10L0 10L0 11L3 11L3 12L2 12L2 13L8 13L8 14L9 14L9 16L10 16L10 17L8 17L8 21L9 21L9 19L10 19L10 17L12 17L12 16L13 16L13 19L12 19L12 18L11 18L11 21L14 21L14 20L15 20L15 19L14 19L14 18L15 18L15 17L14 17L14 16L13 16L13 15L11 15L11 13L12 13L12 12L13 12L13 9L14 9L14 8L13 8L13 9L12 9L12 12L10 12L10 14L9 14L9 12L8 12L8 11L9 11L9 10L10 10L10 9L11 9L11 6L10 6L10 7L9 7L9 6ZM12 6L12 7L13 7L13 6ZM9 8L9 9L10 9L10 8ZM16 8L16 10L14 10L14 11L16 11L16 10L18 10L18 9L19 9L19 8ZM20 8L20 9L21 9L21 8ZM2 9L2 10L3 10L3 11L4 11L4 9ZM19 10L19 11L21 11L21 10ZM6 11L6 12L7 12L7 11ZM17 11L17 12L18 12L18 11ZM0 12L0 13L1 13L1 12ZM14 12L14 13L13 13L13 14L14 14L14 15L15 15L15 16L17 16L17 17L16 17L16 18L18 18L18 19L19 19L19 18L20 18L20 17L19 17L19 15L17 15L17 13L16 13L16 12ZM20 12L20 13L19 13L19 14L20 14L20 13L21 13L21 12ZM14 13L14 14L15 14L15 13ZM20 15L20 16L21 16L21 15ZM13 19L13 20L14 20L14 19ZM20 19L20 20L21 20L21 19ZM17 20L17 21L18 21L18 20ZM0 0L0 7L7 7L7 0ZM1 1L1 6L6 6L6 1ZM2 2L2 5L5 5L5 2ZM14 0L14 7L21 7L21 0ZM15 1L15 6L20 6L20 1ZM16 2L16 5L19 5L19 2ZM0 14L0 21L7 21L7 14ZM1 15L1 20L6 20L6 15ZM2 16L2 19L5 19L5 16Z\" fill=\"#000000\"/></g></g></svg>\n"
    }
  }
}
```

-失敗

#### 沒有權限

```json
{
  "result": false,
  "msg": ["You do not have permission to access this resource."]
}
```

### course_qas/{id}/actions/run(POST)-開始課堂搶答

#### Request

- Method: **POST**
- URL: `course_qas/{id}/actions/run`
- Headers: Content-Type:multipart/form-data
- Path-params:

| 名稱         | 類型 | 說明         | 範例 | 是否必須 |
| :----------- | :--- | :----------- | :--- | :------- |
| course_id    | int  | 課堂 ID      | 1    | O        |
| Bearer Token |      | 要為老師身分 |      | O        |

- 狀態說明
  課堂搶答執行此 API 成功後狀態會更新為 running

#### Response

-成功

- Body:

```json
{
  "result": true,
  "msg": ["Success"],
  "data": {
    "id": 8
  }
}
```

-失敗

#### 沒有權限(不是老師)

- Status: 403 Forbidden
- Body:

```json
{
  "result": false,
  "msg": ["You do not have permission to access this resource."]
}
```

#### MQTT

```json
{
  "course_data": "略",
  "status": "qa_answering",
  "api": "course_qas/{id}/actions/answer",
  "method": "post",
  "course_stu_ids": []
}
```

### course_qas/{id}/actions/stop(POST)-停止課堂搶答

#### Request

- Method: **POST**
- URL: `course_qas/{id}/actions/stop`
- Headers: Content-Type:multipart/form-data
- Path-params:

| 名稱         | 類型 | 說明         | 範例 | 是否必須 |
| :----------- | :--- | :----------- | :--- | :------- |
| course_id    | int  | 課堂 ID      | 1    | O        |
| Bearer Token |      | 要為老師身分 |      | O        |

- 狀態說明
  課堂搶答執行此 API 成功後狀態會更新為 stopped

#### Response

-成功

- Body:

```json
{
  "result": true,
  "msg": ["Success"],
  "data": {
    "id": 8
  }
}
```

-失敗

#### 沒有權限(不是老師)

- Status: 403 Forbidden
- Body:

```json
{
  "result": false,
  "msg": ["You do not have permission to access this resource."]
}
```

#### MQTT

```json
{
  "course_data": "略",
  "status": "qa_stopped",
  "api": "",
  "method": "",
  "course_stu_ids": []
}
```

### course_qas/{id}/actions/time_up(POST)-結束課堂搶答

#### Request

- Method: **POST**
- URL: `course_qas/{id}/actions/time_up`
- Headers: Content-Type:multipart/form-data
- Path-params:

| 名稱         | 類型 | 說明         | 範例 | 是否必須 |
| :----------- | :--- | :----------- | :--- | :------- |
| course_id    | int  | 課堂 ID      | 1    | O        |
| Bearer Token |      | 要為老師身分 |      | O        |

- 狀態說明
  課堂搶答執行此 API 成功後狀態會更新為 time_up

#### Response

-成功

- Body:

```json
{
  "result": true,
  "msg": ["Success"],
  "data": {
    "id": 8
  }
}
```

-失敗

#### 沒有權限(不是老師)

- Status: 403 Forbidden
- Body:

```json
{
  "result": false,
  "msg": ["You do not have permission to access this resource."]
}
```

#### MQTT

```json
{
  "course_data": "略",
  "status": "qa_time_up",
  "api": "",
  "method": "",
  "course_stu_ids": []
}
```

### course_qas/{id}/actions/answer(POST)-學生回答課堂搶答

#### Request

- Method: **POST**
- URL: `course_qas/{id}/actions/answer`
- Headers: Content-Type:multipart/form-data
- Path-params:

| 名稱         | 類型   | 說明                                                    | 範例                                | 是否必須             |
| :----------- | :----- | :------------------------------------------------------ | :---------------------------------- | :------------------- |
| id           | int    | 課堂搶答 ID                                             | 120                                 | O                    |
| answer       | string | 回答 只可回答以下內容(1,2,3,4,5,6,7,8,9,10,A,B,C,D,O,X) | 3                                   | X (competition 必須) |
| Bearer Token |        | 有登入的學生必須要                                      |                                     | X                    |
| token        |        | 訪客學生必須要                                          | 10-d401f35993b3f038d24c552b9b3c3a53 | X                    |

- 狀態說明
  執行此 API 時搶答狀態須為 running 才會成功

#### Response

-成功

- Body:

```json
{
  "result": true,
  "msg": ["Success"],
  "data": []
}
```

-失敗

#### 沒有權限

- Status: 403 Forbidden
- Body:

```json
{
  "result": false,
  "msg": ["You do not have permission to access this resource."]
}
```

#### 答案格式錯誤(競賽)

```json
{
  "result": false,
  "msg": ["answer:The selected answer is invalid."]
}
```

#### 已經回答過(競賽)

```json
{
  "result": false,
  "msg": ["Answer already exists."]
}
```

#### 目前不是搶答階段(或已經被別人搶答成功)

```json
{
  "result": false,
  "msg": ["The Qa is not in running status."]
}
```

#### MQTT

```json
{
  "course_data": "略",
  "status": "qa_answered_success",
  "api": "course_qas/{id}/actions/get_result",
  "method": "get",
  "course_stu_ids": []
}
```

### course_qas/{id}/actions/publish_answer(POST)-老師公布競賽搶答答案

#### Request

- Method: **GET**
- URL: `course_qas/{id}/actions/publish_answer`
- Headers:
- Path-params:

| 名稱           | 類型   | 說明                                                    | 範例 | 是否必須 |
| :------------- | :----- | :------------------------------------------------------ | :--- | :------- |
| id             | int    | 課堂搶答 ID                                             | 1    | O        |
| correct_answer | string | 答案 只可回答以下內容(1,2,3,4,5,6,7,8,9,10,A,B,C,D,O,X) | 1    | O        |
| Bearer Token   |        |                                                         |      | O        |

- 狀態說明
  課堂搶答會有以下狀態, 執行此 API 時狀態須為 running/stopped 才會成功

#### Response

- params:

| 名稱                | 類型  | 說明                   | 範例             |
| :------------------ | :---- | :--------------------- | :--------------- |
| total_stu_count     | int   | 全班學生數             | 10               |
| alive_stu_count     | int   | 晉級學生數             | 3                |
| not_alive_stu_count | int   | 淘汰學生數             | 7                |
| course_qa_stus      | array | 全班學生搶答狀態與資料 | 參考下方執行結果 |

-成功

- Body:

```json
{
  "result": true,
  "msg": ["Success"],
  "data": {
    "total_stu_count": 9,
    "alive_stu_count": 0,
    "not_alive_stu_count": 9,
    "course_qa_stus": [
      {
        "id": 37,
        "course_qa_id": 7,
        "course_stu_id": 4,
        "answer": null,
        "is_alive": 0,
        "created_at": "2024-02-05 21:18:01",
        "updated_at": "2024-02-05 22:14:39",
        "deleted_at": null,
        "course_stu": {
          "id": 4,
          "course_id": 1,
          "user_id": 0,
          "nickname": "小火",
          "is_visitor": 1,
          "score": 5,
          "avatar_file_id": 1,
          "is_online": 1,
          "created_at": "2023-12-30 11:39:56",
          "updated_at": "2023-12-30 11:39:56",
          "deleted_at": null,
          "stream_url": null,
          "comment": "",
          "avatar_file": {
            "id": 1,
            "uploader_id": 0,
            "uploader_type": "student",
            "file_type": "image",
            "course_id": 1,
            "drive_id": "GOMQXKw0NRF5CAq3HBOk7fx1cntuk1sxrirZDoCV.png",
            "created_at": "2023-12-30 11:32:58",
            "updated_at": "2023-12-30 11:32:58",
            "deleted_at": null
          }
        }
      },
      {
        "id": 38,
        "course_qa_id": 7,
        "course_stu_id": 5,
        "answer": null,
        "is_alive": 0,
        "created_at": "2024-02-05 21:18:01",
        "updated_at": "2024-02-05 22:14:39",
        "deleted_at": null,
        "course_stu": {
          "id": 5,
          "course_id": 1,
          "user_id": 0,
          "nickname": "小土",
          "is_visitor": 1,
          "score": 10,
          "avatar_file_id": 1,
          "is_online": 1,
          "created_at": "2023-12-30 13:06:05",
          "updated_at": "2024-01-19 11:17:15",
          "deleted_at": null,
          "stream_url": null,
          "comment": "",
          "avatar_file": {
            "id": 1,
            "uploader_id": 0,
            "uploader_type": "student",
            "file_type": "image",
            "course_id": 1,
            "drive_id": "GOMQXKw0NRF5CAq3HBOk7fx1cntuk1sxrirZDoCV.png",
            "created_at": "2023-12-30 11:32:58",
            "updated_at": "2023-12-30 11:32:58",
            "deleted_at": null
          }
        }
      },
      {
        "id": 39,
        "course_qa_id": 7,
        "course_stu_id": 7,
        "answer": null,
        "is_alive": 0,
        "created_at": "2024-02-05 21:18:01",
        "updated_at": "2024-02-05 22:14:39",
        "deleted_at": null,
        "course_stu": {
          "id": 7,
          "course_id": 1,
          "user_id": 3,
          "nickname": "晶晶",
          "is_visitor": 0,
          "score": 0,
          "avatar_file_id": 1,
          "is_online": 1,
          "created_at": "2024-01-03 17:23:21",
          "updated_at": "2024-01-03 17:23:21",
          "deleted_at": null,
          "stream_url": null,
          "comment": "",
          "avatar_file": {
            "id": 1,
            "uploader_id": 0,
            "uploader_type": "student",
            "file_type": "image",
            "course_id": 1,
            "drive_id": "GOMQXKw0NRF5CAq3HBOk7fx1cntuk1sxrirZDoCV.png",
            "created_at": "2023-12-30 11:32:58",
            "updated_at": "2023-12-30 11:32:58",
            "deleted_at": null
          }
        }
      },
      {
        "id": 40,
        "course_qa_id": 7,
        "course_stu_id": 9,
        "answer": null,
        "is_alive": 0,
        "created_at": "2024-02-05 21:18:01",
        "updated_at": "2024-02-05 22:14:39",
        "deleted_at": null,
        "course_stu": {
          "id": 9,
          "course_id": 1,
          "user_id": 0,
          "nickname": "甜甜",
          "is_visitor": 1,
          "score": 0,
          "avatar_file_id": 2,
          "is_online": 1,
          "created_at": "2024-01-04 12:00:57",
          "updated_at": "2024-01-04 12:00:57",
          "deleted_at": null,
          "stream_url": null,
          "comment": "",
          "avatar_file": {
            "id": 2,
            "uploader_id": 2,
            "uploader_type": "teacher",
            "file_type": "image",
            "course_id": 1,
            "drive_id": "3bMh2q7veqawRhojKPbekym3qmf4p7DMvAb4FG8E.png",
            "created_at": "2024-01-05 16:19:46",
            "updated_at": "2024-01-05 16:19:46",
            "deleted_at": null
          }
        }
      },
      {
        "id": 41,
        "course_qa_id": 7,
        "course_stu_id": 10,
        "answer": null,
        "is_alive": 0,
        "created_at": "2024-02-05 21:18:01",
        "updated_at": "2024-02-05 22:14:39",
        "deleted_at": null,
        "course_stu": {
          "id": 10,
          "course_id": 1,
          "user_id": 0,
          "nickname": "心心",
          "is_visitor": 1,
          "score": 0,
          "avatar_file_id": 4,
          "is_online": 1,
          "created_at": "2024-01-13 17:25:22",
          "updated_at": "2024-01-13 17:25:22",
          "deleted_at": null,
          "stream_url": null,
          "comment": "",
          "avatar_file": {
            "id": 4,
            "uploader_id": 2,
            "uploader_type": "teacher",
            "file_type": "image",
            "course_id": 1,
            "drive_id": "xFB9bvDOHPCzw2cJJucyeGbep40POZCyEcOjWXkU.png",
            "created_at": "2024-01-05 16:22:37",
            "updated_at": "2024-01-05 16:22:37",
            "deleted_at": null
          }
        }
      },
      {
        "id": 42,
        "course_qa_id": 7,
        "course_stu_id": 11,
        "answer": null,
        "is_alive": 0,
        "created_at": "2024-02-05 21:18:01",
        "updated_at": "2024-02-05 22:14:39",
        "deleted_at": null,
        "course_stu": {
          "id": 11,
          "course_id": 1,
          "user_id": 0,
          "nickname": "心心",
          "is_visitor": 1,
          "score": 0,
          "avatar_file_id": 3,
          "is_online": 1,
          "created_at": "2024-01-14 13:40:45",
          "updated_at": "2024-01-14 13:40:45",
          "deleted_at": null,
          "stream_url": null,
          "comment": "",
          "avatar_file": {
            "id": 3,
            "uploader_id": 2,
            "uploader_type": "teacher",
            "file_type": "image",
            "course_id": 1,
            "drive_id": "UvbfL0W9iZoIuaXoAcf1qR7MgMGcmAyITLZzKU1R.png",
            "created_at": "2024-01-05 16:21:44",
            "updated_at": "2024-01-05 16:21:44",
            "deleted_at": null
          }
        }
      },
      {
        "id": 43,
        "course_qa_id": 7,
        "course_stu_id": 12,
        "answer": null,
        "is_alive": 0,
        "created_at": "2024-02-05 21:18:01",
        "updated_at": "2024-02-05 22:14:39",
        "deleted_at": null,
        "course_stu": {
          "id": 12,
          "course_id": 1,
          "user_id": 3,
          "nickname": "小明",
          "is_visitor": 0,
          "score": 0,
          "avatar_file_id": 32,
          "is_online": 1,
          "created_at": "2024-01-14 13:46:10",
          "updated_at": "2024-01-14 13:46:10",
          "deleted_at": null,
          "stream_url": null,
          "comment": "",
          "avatar_file": {
            "id": 32,
            "uploader_id": 2,
            "uploader_type": "teacher",
            "file_type": "image",
            "course_id": 1,
            "drive_id": "het8OkZJOayqSafvFp5PjudHpzEMKoMqg7b0JEcO.png",
            "created_at": "2024-01-06 19:30:06",
            "updated_at": "2024-01-06 19:30:06",
            "deleted_at": null
          }
        }
      },
      {
        "id": 44,
        "course_qa_id": 7,
        "course_stu_id": 13,
        "answer": null,
        "is_alive": 0,
        "created_at": "2024-02-05 21:18:01",
        "updated_at": "2024-02-05 22:14:39",
        "deleted_at": null,
        "course_stu": {
          "id": 13,
          "course_id": 1,
          "user_id": 0,
          "nickname": "心心",
          "is_visitor": 1,
          "score": 0,
          "avatar_file_id": 2,
          "is_online": 1,
          "created_at": "2024-01-14 14:31:34",
          "updated_at": "2024-01-14 14:31:34",
          "deleted_at": null,
          "stream_url": null,
          "comment": "",
          "avatar_file": {
            "id": 2,
            "uploader_id": 2,
            "uploader_type": "teacher",
            "file_type": "image",
            "course_id": 1,
            "drive_id": "3bMh2q7veqawRhojKPbekym3qmf4p7DMvAb4FG8E.png",
            "created_at": "2024-01-05 16:19:46",
            "updated_at": "2024-01-05 16:19:46",
            "deleted_at": null
          }
        }
      },
      {
        "id": 45,
        "course_qa_id": 7,
        "course_stu_id": 15,
        "answer": null,
        "is_alive": 0,
        "created_at": "2024-02-05 21:18:01",
        "updated_at": "2024-02-05 22:14:39",
        "deleted_at": null,
        "course_stu": {
          "id": 15,
          "course_id": 1,
          "user_id": 0,
          "nickname": "心心",
          "is_visitor": 1,
          "score": 0,
          "avatar_file_id": 5,
          "is_online": 1,
          "created_at": "2024-01-16 22:36:33",
          "updated_at": "2024-01-16 22:36:33",
          "deleted_at": null,
          "stream_url": null,
          "comment": "",
          "avatar_file": {
            "id": 5,
            "uploader_id": 2,
            "uploader_type": "teacher",
            "file_type": "image",
            "course_id": 1,
            "drive_id": "BJ3pCI1q4AbgWNtpNfQLyU0nKg2rg6Nkd9z3sUM7.png",
            "created_at": "2024-01-05 16:23:54",
            "updated_at": "2024-01-05 16:23:54",
            "deleted_at": null
          }
        }
      }
    ]
  }
}
```

-失敗

#### 不是該堂課的老師

- Body

```json
{
  "result": false,
  "msg": ["You do not have permission to access this resource."]
}
```

#### MQTT

```json
{
  "course_data": "略",
  "status": "qa_complete",
  "api": "course_qas/7/actions/get_result",
  "method": "get",
  "course_stu_ids": []
}
```

### course_qas/{id}/actions/get_result(GET)-取得目前競賽搶答狀況

#### Request

- Method: **GET**
- URL: `course_qas/{id}/actions/get_result`
- Headers:
- Path-params:

| 名稱         | 類型 | 說明                    | 範例                                | 是否必須 |
| :----------- | :--- | :---------------------- | :---------------------------------- | :------- |
| id           | int  | 課堂搶答 ID             | 1                                   | O        |
| Bearer Token |      | 有登入的學生/老師必須要 |                                     | X        |
| token        |      | 訪客學生必須要          | 10-d401f35993b3f038d24c552b9b3c3a53 | X        |

#### Response

競賽搶答會回傳各狀態學生數、各學生狀態
加分搶答會回傳最後一次搶答成功的學生

- params:

| 名稱                | 類型  | 說明                   | 範例             |
| :------------------ | :---- | :--------------------- | :--------------- |
| total_stu_count     | int   | 全班學生數             | 10               |
| alive_stu_count     | int   | 晉級學生數             | 3                |
| not_alive_stu_count | int   | 淘汰學生數             | 7                |
| course_qa_stus      | array | 全班學生搶答狀態與資料 | 參考下方執行結果 |

-成功

- Body:

```json (競賽搶答)
{
  "result": true,
  "msg": ["Success"],
  "data": {
    "total_stu_count": 8,
    "alive_stu_count": 0,
    "not_alive_stu_count": 8,
    "course_qa_stus": [
      {
        "id": 1,
        "course_qa_id": 3,
        "course_stu_id": 4,
        "answer": null,
        "is_alive": 0,
        "created_at": "2024-02-04 13:01:52",
        "updated_at": "2024-02-05 14:51:31",
        "deleted_at": null,
        "course_stu": {
          "id": 4,
          "course_id": 1,
          "user_id": 0,
          "nickname": "小火",
          "is_visitor": 1,
          "score": 5,
          "avatar_file_id": 1,
          "is_online": 1,
          "created_at": "2023-12-30 11:39:56",
          "updated_at": "2023-12-30 11:39:56",
          "deleted_at": null,
          "stream_url": null,
          "comment": "",
          "avatar_file": {
            "id": 1,
            "uploader_id": 0,
            "uploader_type": "student",
            "file_type": "image",
            "course_id": 1,
            "drive_id": "GOMQXKw0NRF5CAq3HBOk7fx1cntuk1sxrirZDoCV.png",
            "created_at": "2023-12-30 11:32:58",
            "updated_at": "2023-12-30 11:32:58",
            "deleted_at": null
          }
        }
      },
      {
        "id": 2,
        "course_qa_id": 3,
        "course_stu_id": 5,
        "answer": null,
        "is_alive": 0,
        "created_at": "2024-02-04 13:01:52",
        "updated_at": "2024-02-05 14:51:31",
        "deleted_at": null,
        "course_stu": {
          "id": 5,
          "course_id": 1,
          "user_id": 0,
          "nickname": "小土",
          "is_visitor": 1,
          "score": 10,
          "avatar_file_id": 1,
          "is_online": 1,
          "created_at": "2023-12-30 13:06:05",
          "updated_at": "2024-01-19 11:17:15",
          "deleted_at": null,
          "stream_url": null,
          "comment": "",
          "avatar_file": {
            "id": 1,
            "uploader_id": 0,
            "uploader_type": "student",
            "file_type": "image",
            "course_id": 1,
            "drive_id": "GOMQXKw0NRF5CAq3HBOk7fx1cntuk1sxrirZDoCV.png",
            "created_at": "2023-12-30 11:32:58",
            "updated_at": "2023-12-30 11:32:58",
            "deleted_at": null
          }
        }
      },
      {
        "id": 3,
        "course_qa_id": 3,
        "course_stu_id": 7,
        "answer": null,
        "is_alive": 0,
        "created_at": "2024-02-04 13:01:52",
        "updated_at": "2024-02-05 14:51:31",
        "deleted_at": null,
        "course_stu": {
          "id": 7,
          "course_id": 1,
          "user_id": 3,
          "nickname": "晶晶",
          "is_visitor": 0,
          "score": 0,
          "avatar_file_id": 1,
          "is_online": 1,
          "created_at": "2024-01-03 17:23:21",
          "updated_at": "2024-01-03 17:23:21",
          "deleted_at": null,
          "stream_url": null,
          "comment": "",
          "avatar_file": {
            "id": 1,
            "uploader_id": 0,
            "uploader_type": "student",
            "file_type": "image",
            "course_id": 1,
            "drive_id": "GOMQXKw0NRF5CAq3HBOk7fx1cntuk1sxrirZDoCV.png",
            "created_at": "2023-12-30 11:32:58",
            "updated_at": "2023-12-30 11:32:58",
            "deleted_at": null
          }
        }
      },
      {
        "id": 4,
        "course_qa_id": 3,
        "course_stu_id": 9,
        "answer": null,
        "is_alive": 0,
        "created_at": "2024-02-04 13:01:52",
        "updated_at": "2024-02-05 14:51:31",
        "deleted_at": null,
        "course_stu": {
          "id": 9,
          "course_id": 1,
          "user_id": 0,
          "nickname": "甜甜",
          "is_visitor": 1,
          "score": 0,
          "avatar_file_id": 2,
          "is_online": 1,
          "created_at": "2024-01-04 12:00:57",
          "updated_at": "2024-01-04 12:00:57",
          "deleted_at": null,
          "stream_url": null,
          "comment": "",
          "avatar_file": {
            "id": 2,
            "uploader_id": 2,
            "uploader_type": "teacher",
            "file_type": "image",
            "course_id": 1,
            "drive_id": "3bMh2q7veqawRhojKPbekym3qmf4p7DMvAb4FG8E.png",
            "created_at": "2024-01-05 16:19:46",
            "updated_at": "2024-01-05 16:19:46",
            "deleted_at": null
          }
        }
      },
      {
        "id": 5,
        "course_qa_id": 3,
        "course_stu_id": 10,
        "answer": null,
        "is_alive": 0,
        "created_at": "2024-02-04 13:01:52",
        "updated_at": "2024-02-05 14:51:31",
        "deleted_at": null,
        "course_stu": {
          "id": 10,
          "course_id": 1,
          "user_id": 0,
          "nickname": "心心",
          "is_visitor": 1,
          "score": 0,
          "avatar_file_id": 4,
          "is_online": 1,
          "created_at": "2024-01-13 17:25:22",
          "updated_at": "2024-01-13 17:25:22",
          "deleted_at": null,
          "stream_url": null,
          "comment": "",
          "avatar_file": {
            "id": 4,
            "uploader_id": 2,
            "uploader_type": "teacher",
            "file_type": "image",
            "course_id": 1,
            "drive_id": "xFB9bvDOHPCzw2cJJucyeGbep40POZCyEcOjWXkU.png",
            "created_at": "2024-01-05 16:22:37",
            "updated_at": "2024-01-05 16:22:37",
            "deleted_at": null
          }
        }
      },
      {
        "id": 6,
        "course_qa_id": 3,
        "course_stu_id": 11,
        "answer": null,
        "is_alive": 0,
        "created_at": "2024-02-04 13:01:52",
        "updated_at": "2024-02-05 14:51:31",
        "deleted_at": null,
        "course_stu": {
          "id": 11,
          "course_id": 1,
          "user_id": 0,
          "nickname": "心心",
          "is_visitor": 1,
          "score": 0,
          "avatar_file_id": 3,
          "is_online": 1,
          "created_at": "2024-01-14 13:40:45",
          "updated_at": "2024-01-14 13:40:45",
          "deleted_at": null,
          "stream_url": null,
          "comment": "",
          "avatar_file": {
            "id": 3,
            "uploader_id": 2,
            "uploader_type": "teacher",
            "file_type": "image",
            "course_id": 1,
            "drive_id": "UvbfL0W9iZoIuaXoAcf1qR7MgMGcmAyITLZzKU1R.png",
            "created_at": "2024-01-05 16:21:44",
            "updated_at": "2024-01-05 16:21:44",
            "deleted_at": null
          }
        }
      },
      {
        "id": 7,
        "course_qa_id": 3,
        "course_stu_id": 12,
        "answer": null,
        "is_alive": 0,
        "created_at": "2024-02-04 13:01:52",
        "updated_at": "2024-02-05 14:51:31",
        "deleted_at": null,
        "course_stu": {
          "id": 12,
          "course_id": 1,
          "user_id": 3,
          "nickname": "小明",
          "is_visitor": 0,
          "score": 0,
          "avatar_file_id": 32,
          "is_online": 1,
          "created_at": "2024-01-14 13:46:10",
          "updated_at": "2024-01-14 13:46:10",
          "deleted_at": null,
          "stream_url": null,
          "comment": "",
          "avatar_file": {
            "id": 32,
            "uploader_id": 2,
            "uploader_type": "teacher",
            "file_type": "image",
            "course_id": 1,
            "drive_id": "het8OkZJOayqSafvFp5PjudHpzEMKoMqg7b0JEcO.png",
            "created_at": "2024-01-06 19:30:06",
            "updated_at": "2024-01-06 19:30:06",
            "deleted_at": null
          }
        }
      },
      {
        "id": 8,
        "course_qa_id": 3,
        "course_stu_id": 13,
        "answer": null,
        "is_alive": 0,
        "created_at": "2024-02-04 13:01:52",
        "updated_at": "2024-02-05 14:51:31",
        "deleted_at": null,
        "course_stu": {
          "id": 13,
          "course_id": 1,
          "user_id": 0,
          "nickname": "心心",
          "is_visitor": 1,
          "score": 0,
          "avatar_file_id": 2,
          "is_online": 1,
          "created_at": "2024-01-14 14:31:34",
          "updated_at": "2024-01-14 14:31:34",
          "deleted_at": null,
          "stream_url": null,
          "comment": "",
          "avatar_file": {
            "id": 2,
            "uploader_id": 2,
            "uploader_type": "teacher",
            "file_type": "image",
            "course_id": 1,
            "drive_id": "3bMh2q7veqawRhojKPbekym3qmf4p7DMvAb4FG8E.png",
            "created_at": "2024-01-05 16:19:46",
            "updated_at": "2024-01-05 16:19:46",
            "deleted_at": null
          }
        }
      }
    ]
  }
}
```

```json (加分搶答)
{
  "result": true,
  "msg": ["Success"],
  "data": {
    "id": 13,
    "course_id": 1,
    "user_id": 0,
    "nickname": "心心",
    "is_visitor": 1,
    "score": 0,
    "avatar_file_id": 2,
    "is_online": 1,
    "created_at": "2024-01-14 14:31:34",
    "updated_at": "2024-01-14 14:31:34",
    "deleted_at": null,
    "stream_url": null,
    "comment": "",
    "avatar_file": {
      "id": 2,
      "uploader_id": 2,
      "uploader_type": "teacher",
      "file_type": "image",
      "course_id": 1,
      "drive_id": "3bMh2q7veqawRhojKPbekym3qmf4p7DMvAb4FG8E.png",
      "created_at": "2024-01-05 16:19:46",
      "updated_at": "2024-01-05 16:19:46",
      "deleted_at": null
    }
  }
}
```

-失敗

#### 沒有權限

```json
{
  "result": false,
  "msg": ["You do not have permission to access this resource."]
}
```

### course_qas/{id}/actions/get_stu_status(GET)-取得學生個人課堂搶答狀態

#### Request

- Method: **GET**
- URL: `course_qas/{id}/actions/get_stu_status`
- Headers:
- Path-params:

| 名稱         | 類型 | 說明                    | 範例                                | 是否必須 |
| :----------- | :--- | :---------------------- | :---------------------------------- | :------- |
| id           | int  | 課堂搶答 ID             | 1                                   | O        |
| Bearer Token |      | 有登入的學生/老師必須要 |                                     | X        |
| token        |      | 訪客學生必須要          | 10-d401f35993b3f038d24c552b9b3c3a53 | X        |

- return-params:

| 名稱   | 類型  | 說明                                        |
| :----- | :---- | :------------------------------------------ |
| data   | int   | 如 api 是 get 類型，會先傳該 api 回覆的資料 |
| status | int   | 參考以下說明                                |
| api    | int   | api 路徑                                    |
| method | array | api 方法                                    |

- [回傳內容說明參考](#課堂搶答學生取得個人化狀態)

#### Response

-成功

- Body:

```json
{
  "result": true,
  "msg": ["Success"],
  "data": [],
  "status": "qa_time_up",
  "api": "",
  "method": ""
}
```

-失敗

#### 沒有權限

```json
{
  "result": false,
  "msg": ["You do not have permission to access this resource."]
}
```

### 課堂評量-MQTT/取得學生個人化狀態說明

#### 教師:課堂評量發送 MQTT

| 時機                                                                 | status                | api                                          | method | 課堂評量 status |
| :------------------------------------------------------------------- | :-------------------- | :------------------------------------------- | :----- | :-------------- |
| 老師執行 API `course_assessments/{id}/actions/run` 成功後            | assessment_initial    | `course_assessments/{id}`                    | get    | initial         |
| 老師執行 API `course_assessments/{id}/actions/stop` 成功後           | assessment_stopped    |                                              |        | stopped         |
| 老師執行 API `course_assessments/{id}/actions/collect` 成功後        | assessment_collected  |                                              |        | collected       |
| 老師執行 API `course_assessments/{id}/actions/restart` 成功後        | assessment_initial    | `course_assessments/{id}`                    | post   | initial         |
| 老師執行 API `course_assessments/{id}/actions/correct` 成功後        | assessment_correcting |                                              |        | correcting      |
| 老師執行 API `course_assessments/{id}/actions/publish_answer` 成功後 | assessment_corrected  | `course_assessments/{id}/actions/get_result` | get    | corrected       |

#### 學生:課堂評量學生取得個人化狀態

| 時機說明                 | status                | api                                          | method | 課堂評量 status |
| :----------------------- | :-------------------- | :------------------------------------------- | :----- | :-------------- |
| 評量未開始               | assessment_closed     |                                              |        | closed          |
| 評量開始   | assessment_initial  | `	course_assessments/{id} `    | get   | initial         |
| 評量被中止               | assessment_stopped    |                                              |        | stopped         |
| 評量答題中, 學生還沒回答 | assessment_answering  | `course_assessments/{id}/actions/answer `    | post   | running         |
| 評量答題中, 學生已回答   | assessment_answered   |                                              |        | running         |
| 評量已收卷               | assessment_collected  |                                              |        | collected       |
| 評量檢討中               | assessment_correcting |                                              |        | correcting      |
| 評量檢討完               | assessment_corrected  | `course_assessments/{id}/actions/get_result` |        | corrected       |

### course_assessments/create(POST)-建立課堂評量

#### Request

- Method: **POST**
- URL: `course_assessments/create`
- Headers: Content-Type:multipart/form-data
- Path-params:

| 名稱         | 類型   | 說明                                                                                | 範例   | 是否必須 |
| :----------- | :----- | :---------------------------------------------------------------------------------- | :----- | :------- |
| course_id    | int    | 課堂 ID                                                                             | 1      | O        |
| quest_type   | string | 值可為 single(單選題),multiple(複選題),tf(是非題),essay(文字題),handwritten(手寫題) | single | O        |
| Bearer Token |        | 要為老師身分才可建立                                                                |        | O        |

- 狀態說明
  課堂評量執行此 API 成功後狀態會更新為 closed

#### Response

-成功

- Body:

```json
{
  "result": true,
  "msg": ["Success"],
  "data": {
    "id": 2
  }
}
```

-失敗

#### 沒有權限(不是老師)

- Status: 403 Forbidden
- Body:

```json
{
  "result": false,
  "msg": ["You do not have permission to access this resource."]
}
```

### pages/create(POST)-建立課堂評量頁面

#### Request

- Method: **POST**
- URL: `pages/create`
- Headers: Content-Type:multipart/form-data
- Path-params:

| 名稱                 | 類型       | 說明                                             | 範例   | 是否必須             |
| :------------------- | :--------- | :----------------------------------------------- | :----- | :------------------- |
| course_assessment_id | int        | 課堂評量 ID                                      | 1      | O                    |
| quest_number         | int        | 此頁問題數量                                     | 3      | O                    |
| page                 | int        | 頁碼                                             | 1      | O                    |
| quest_file           | image file | 題目圖片                                         |        | O                    |
| option_number        | int        | 題目選項數量                                     | 4      | X(單選題/複選題必須) |
| option_type          | string     | 題目選項類型 值可為 number(數字),character(字母) | number | X(單選題/複選題必須) |
| score                | int        | 此頁分數總分 (0~100)                             | 12     | O                    |
| Bearer Token         |            | 要為老師身分才可建立                             |        | O                    |

#### Response

-成功

- Body:

```json
{
  "result": true,
  "msg": ["Success"],
  "data": {
    "id": 8
  }
}
```

-失敗

#### 沒有權限(不是老師)

- Status: 403 Forbidden
- Body:

```json
{
  "result": false,
  "msg": ["You do not have permission to access this resource."]
}
```

### pages/{id}(PUT)-更新課堂評量頁面

#### Request

- Method: **PUT**
- URL: `pages/{id}`
- Headers: Content-Type:multipart/form-data
- Path-params:

| 名稱          | 類型   | 說明                                             | 範例   | 是否必須                 |
| :------------ | :----- | :----------------------------------------------- | :----- | :----------------------- |
| id            | int    | 課堂評量頁面 id                                  | 1      | O                        |
| quest_number  | int    | 此頁問題數量                                     | 3      | X                        |
| option_number | int    | 題目選項數量                                     | 4      | X(單選題/複選題才可更新) |
| option_type   | string | 題目選項類型 值可為 number(數字),character(字母) | number | X(單選題/複選題才可更新) |
| score         | int    | 此頁分數總分 (0~100)                             | 12     | X                        |
| Bearer Token  |        | 要為老師身分才可建立                             |        | O                        |

#### Response

-成功

- Body:

```json
{
  "result": true,
  "msg": ["Success"],
  "data": {
    "id": 8
  }
}
```

-失敗

#### 沒有權限(不是老師)

- Status: 403 Forbidden
- Body:

```json
{
  "result": false,
  "msg": ["You do not have permission to access this resource."]
}
```

### pages/{id}(DELETE)-刪除課堂評量頁面

#### Request

- Method: **DELETE**
- URL: `pages/{id}`
- Headers: Content-Type:multipart/form-data
- Path-params:

| 名稱         | 類型 | 說明                 | 範例 | 是否必須 |
| :----------- | :--- | :------------------- | :--- | :------- |
| id           | int  | 課堂評量頁面 id      | 1    | O        |
| Bearer Token |      | 要為老師身分才可刪除 |      | O        |

- 刪除頁面後，後面的頁面頁碼(page)會自動往前一頁

#### Response

-成功

- Body:

```json
{
  "result": true,
  "msg": ["Success"],
  "data": []
}
```

-失敗

#### 沒有權限(不是老師)

- Status: 403 Forbidden
- Body:

```json
{
  "result": false,
  "msg": ["You do not have permission to access this resource."]
}
```

#### 找不到課堂評量頁面

```json
{
  "result": false,
  "msg": ["Page with id 17 not found."]
}
```

### course_assessments/{id}/actions/run(POST)-開始課堂評量

#### Request

- Method: **POST**
- URL: `course_assessments/{id}/actions/run`
- Headers: Content-Type:multipart/form-data
- Path-params:

| 名稱         | 類型 | 說明         | 範例 | 是否必須 |
| :----------- | :--- | :----------- | :--- | :------- |
| id           | int  | 課堂評量 ID  | 1    | O        |
| Bearer Token |      | 要為老師身分 |      | O        |

- 狀態說明
  課堂評量執行此 API 成功後狀態會更新為 running

#### Response

-成功

- Body:

```json
{
  "result": true,
  "msg": ["Success"],
  "data": []
}
```

-失敗

#### 沒有權限(不是老師)

- Status: 403 Forbidden
- Body:

```json
{
  "result": false,
  "msg": ["You do not have permission to access this resource."]
}
```

#### MQTT

新開始的考試/重新考試

```json
{
  "course_data": "略",
  "status": "assessment_initial",
  "api": "course_assessments/{id}",
  "method": "get",
  "course_stu_ids": []
}
```

從 stop 狀態繼續開始

```json
{
  "course_data": "略",
  "status": "assessment_answering",
  "api": "course_assessments/{id}/actions/answer",
  "method": "post",
  "course_stu_ids": []
}
```

### course_assessments/{id}(GET)-取得課堂評量

#### Request

- Method: **GET**
- URL: `course_assessments/{id}`
- Headers:
- Path-params:

| 名稱         | 類型 | 說明                    | 範例                                | 是否必須 |
| :----------- | :--- | :---------------------- | :---------------------------------- | :------- |
| id           | int  | 課堂評量 ID             | 1                                   | O        |
| Bearer Token |      | 有登入的學生/老師必須要 |                                     | X        |
| token        |      | 訪客學生必須要          | 10-d401f35993b3f038d24c552b9b3c3a53 | X        |

#### Response

- param:

| 名稱               | 類型   | 說明                                              | 範例             |
| :----------------- | :----- | :------------------------------------------------ | :--------------- |
| status             | string | 課堂評量狀態                                      | running          |
| pages              | string | 課堂評量頁面內容                                  | running          |
| pages-question_ids | array  | 課堂評量頁面中所包含的題目 id, 評量未開始時是空的 | [50, 51, 52, 53] |

- status 說明參考[課堂評量-MQTT/取得學生個人化狀態說明](#課堂評量-MQTT/取得學生個人化狀態說明) 課堂評量 status 欄位

-成功

- Body:

```json
{
  "result": true,
  "msg": ["Success"],
  "data": {
    "id": 2,
    "course_id": 1,
    "created_at": "2024-02-14 10:34:53",
    "updated_at": "2024-02-15 10:58:32",
    "deleted_at": null,
    "status": "running",
    "quest_type": "essay",
    "pages": [
      {
        "id": 7,
        "course_assessment_id": 2,
        "quest_number": 4,
        "page": 1,
        "quest_file_id": 94,
        "option_number": 0,
        "option_type": "",
        "score": 12,
        "created_at": "2024-02-15 10:05:06",
        "updated_at": "2024-02-15 10:05:06",
        "deleted_at": null,
        "options": [],
        "question_ids": [50, 51, 52, 53],
        "quest_file": {
          "id": 94,
          "uploader_id": 2,
          "uploader_type": "teacher",
          "file_type": "image",
          "course_id": 1,
          "drive_id": "R1cD83NJYa1l8dwD2NmKXaRiIFldmCi7B4xEFmxE.jpg",
          "created_at": "2024-02-15 10:05:06",
          "updated_at": "2024-02-15 10:05:06",
          "deleted_at": null
        },
        "questions": [
          {
            "id": 50,
            "page_id": 7,
            "answer": null,
            "created_at": "2024-02-15 10:58:32",
            "updated_at": "2024-02-15 10:58:32",
            "deleted_at": null,
            "order": 1
          },
          {
            "id": 51,
            "page_id": 7,
            "answer": null,
            "created_at": "2024-02-15 10:58:32",
            "updated_at": "2024-02-15 10:58:32",
            "deleted_at": null,
            "order": 2
          },
          {
            "id": 52,
            "page_id": 7,
            "answer": null,
            "created_at": "2024-02-15 10:58:32",
            "updated_at": "2024-02-15 10:58:32",
            "deleted_at": null,
            "order": 3
          },
          {
            "id": 53,
            "page_id": 7,
            "answer": null,
            "created_at": "2024-02-15 10:58:32",
            "updated_at": "2024-02-15 10:58:32",
            "deleted_at": null,
            "order": 4
          }
        ]
      },
      {
        "id": 9,
        "course_assessment_id": 2,
        "quest_number": 2,
        "page": 2,
        "quest_file_id": 95,
        "option_number": 0,
        "option_type": "",
        "score": 12,
        "created_at": "2024-02-15 10:07:47",
        "updated_at": "2024-02-15 10:52:07",
        "deleted_at": null,
        "options": [],
        "question_ids": [54, 55],
        "quest_file": {
          "id": 95,
          "uploader_id": 2,
          "uploader_type": "teacher",
          "file_type": "image",
          "course_id": 1,
          "drive_id": "wyg7q9ReTgM4cJShi7vrSHePvpxK6xpo8iTGQ5Z9.jpg",
          "created_at": "2024-02-15 10:07:47",
          "updated_at": "2024-02-15 10:07:47",
          "deleted_at": null
        },
        "questions": [
          {
            "id": 54,
            "page_id": 9,
            "answer": null,
            "created_at": "2024-02-15 10:58:32",
            "updated_at": "2024-02-15 10:58:32",
            "deleted_at": null,
            "order": 1
          },
          {
            "id": 55,
            "page_id": 9,
            "answer": null,
            "created_at": "2024-02-15 10:58:32",
            "updated_at": "2024-02-15 10:58:32",
            "deleted_at": null,
            "order": 2
          }
        ]
      }
    ],
    "course": {
      "id": 1,
      "user_id": 2,
      "class_name": "一年一班",
      "subject": "數學",
      "code": "yMdlXBrpo9",
      "is_open": 1,
      "status": "assessment_answering",
      "created_at": "2023-12-28 11:15:04",
      "updated_at": "2024-02-15 10:58:32",
      "deleted_at": null,
      "status_id": 2,
      "qrcode_svg": "<?xml version=\"1.0\" encoding=\"UTF-8\"?>\n<svg xmlns=\"http://www.w3.org/2000/svg\" version=\"1.1\" width=\"100\" height=\"100\" viewBox=\"0 0 100 100\"><rect x=\"0\" y=\"0\" width=\"100\" height=\"100\" fill=\"#ffffff\"/><g transform=\"scale(4.762)\"><g transform=\"translate(0,0)\"><path fill-rule=\"evenodd\" d=\"M8 0L8 1L9 1L9 2L8 2L8 5L11 5L11 4L12 4L12 3L13 3L13 0L12 0L12 3L11 3L11 2L10 2L10 0ZM9 2L9 4L11 4L11 3L10 3L10 2ZM8 6L8 7L9 7L9 8L8 8L8 9L9 9L9 10L6 10L6 9L7 9L7 8L6 8L6 9L4 9L4 8L0 8L0 9L1 9L1 10L0 10L0 11L3 11L3 12L2 12L2 13L8 13L8 14L9 14L9 16L10 16L10 17L8 17L8 21L9 21L9 19L10 19L10 17L12 17L12 16L13 16L13 19L12 19L12 18L11 18L11 21L14 21L14 20L15 20L15 19L14 19L14 18L15 18L15 17L14 17L14 16L13 16L13 15L11 15L11 13L12 13L12 12L13 12L13 9L14 9L14 8L13 8L13 9L12 9L12 12L10 12L10 14L9 14L9 12L8 12L8 11L9 11L9 10L10 10L10 9L11 9L11 6L10 6L10 7L9 7L9 6ZM12 6L12 7L13 7L13 6ZM9 8L9 9L10 9L10 8ZM16 8L16 10L14 10L14 11L16 11L16 10L18 10L18 9L19 9L19 8ZM20 8L20 9L21 9L21 8ZM2 9L2 10L3 10L3 11L4 11L4 9ZM19 10L19 11L21 11L21 10ZM6 11L6 12L7 12L7 11ZM17 11L17 12L18 12L18 11ZM0 12L0 13L1 13L1 12ZM14 12L14 13L13 13L13 14L14 14L14 15L15 15L15 16L17 16L17 17L16 17L16 18L18 18L18 19L19 19L19 18L20 18L20 17L19 17L19 15L17 15L17 13L16 13L16 12ZM20 12L20 13L19 13L19 14L20 14L20 13L21 13L21 12ZM14 13L14 14L15 14L15 13ZM20 15L20 16L21 16L21 15ZM13 19L13 20L14 20L14 19ZM20 19L20 20L21 20L21 19ZM17 20L17 21L18 21L18 20ZM0 0L0 7L7 7L7 0ZM1 1L1 6L6 6L6 1ZM2 2L2 5L5 5L5 2ZM14 0L14 7L21 7L21 0ZM15 1L15 6L20 6L20 1ZM16 2L16 5L19 5L19 2ZM0 14L0 21L7 21L7 14ZM1 15L1 20L6 20L6 15ZM2 16L2 19L5 19L5 16Z\" fill=\"#000000\"/></g></g></svg>\n"
    }
  }
}
```

-失敗

#### 沒有權限

```json
{
  "result": false,
  "msg": ["You do not have permission to access this resource."]
}
```

### course_assessments/{id}/actions/stop(POST)-停止課堂評量

#### Request

- Method: **POST**
- URL: `course_assessments/{id}/actions/stop`
- Headers: Content-Type:multipart/form-data
- Path-params:

| 名稱         | 類型 | 說明         | 範例 | 是否必須 |
| :----------- | :--- | :----------- | :--- | :------- |
| course_id    | int  | 課堂 ID      | 1    | O        |
| Bearer Token |      | 要為老師身分 |      | O        |

- 狀態說明
  課堂評量執行此 API 成功後狀態會更新為 stopped

#### Response

-成功

- Body:

```json
{
  "result": true,
  "msg": ["Success"],
  "data": []
}
```

-失敗

#### 沒有權限(不是老師)

- Status: 403 Forbidden
- Body:

```json
{
  "result": false,
  "msg": ["You do not have permission to access this resource."]
}
```

#### MQTT

```json
{
  "course_data": "略",
  "status": "assessment_stopped",
  "api": "",
  "method": "",
  "course_stu_ids": []
}
```

### course_assessments/{id}/actions/restart(POST)-重新作答課堂評量

#### Request

- Method: **POST**
- URL: `course_assessments/{id}/actions/restart`
- Headers: Content-Type:multipart/form-data
- Path-params:

| 名稱         | 類型 | 說明         | 範例 | 是否必須 |
| :----------- | :--- | :----------- | :--- | :------- |
| course_id    | int  | 課堂 ID      | 1    | O        |
| Bearer Token |      | 要為老師身分 |      | O        |

- 狀態說明
  課堂評量執行此 API 成功後狀態會更新為 running

#### Response

-成功

- Body:

```json
{
  "result": true,
  "msg": ["Success"],
  "data": []
}
```

-失敗

#### 沒有權限(不是老師)

- Status: 403 Forbidden
- Body:

```json
{
  "result": false,
  "msg": ["You do not have permission to access this resource."]
}
```

#### MQTT

```json
{
  "course_data": "略",
  "status": "assessment_initial",
  "api": "course_assessments/{id}",
  "method": "get",
  "course_stu_ids": {}
}
```

### course_assessments/{id}/actions/answer(POST)-學生回答課堂評量

#### Request

- Method: **POST**
- URL: `course_assessments/{id}/actions/answer`
- Headers: Content-Type:multipart/form-data
- Path-params:

| 名稱                   | 類型        | 說明               | 範例                                | 是否必須 |
| :--------------------- | :---------- | :----------------- | :---------------------------------- | :------- |
| id                     | int         | 課堂評量 ID        | 120                                 | O        |
| {question_id}:{answer} | string/file | 問題 ID 對應回答   | "50":"answer1"                      | X        |
| Bearer Token           |             | 有登入的學生必須要 |                                     | X        |
| token                  |             | 訪客學生必須要     | 10-d401f35993b3f038d24c552b9b3c3a53 | X        |

- 狀態說明
  執行此 API 時課堂評量狀態須為 running 才能回答

- 只能回答一次, 回答過不可再回答

```json
{
  "50": "ans1",
  "51": "ans2",
  "52": "ans3",
  "53": "ans4"
}
```

#### Response

-成功

- Body:

```json
{
  "result": true,
  "msg": ["Success"],
  "data": []
}
```

-失敗

#### 沒有權限

- Status: 403 Forbidden
- Body:

```json
{
  "result": false,
  "msg": ["You do not have permission to access this resource."]
}
```

#### 答案選項格式錯誤 (EX:字母回答成數字)

```json
{
  "result": false,
  "msg": ["Answer option type error:19, 23"]
}
```

#### 已經回答過

```json
{
  "result": false,
  "msg": ["The student is already answered."]
}
```

#### 目前不是回答階段

```json
{
  "result": false,
  "msg": ["The assessment is not in running status."]
}
```

#### 題目 ID 錯誤

```json
{
  "result": false,
  "msg": ["Question id not found:19, 23"]
}
```

#### MQTT

- nickname:交卷學生暱稱
- finished_stu_total:目前已交卷數量

```json
{
  "course_data": "略",
  "status": "course_stu_finished_assessment",
  "api": "",
  "method": "",
  "course_stu_ids": [],
  "nickname": "Alex",
  "finished_stu_total": 4
}
```

### course_assessments/{id}/actions/collect(POST)-收卷課堂評量

#### Request

- Method: **POST**
- URL: `course_assessments/{id}/actions/collect`
- Headers: Content-Type:multipart/form-data
- Path-params:

| 名稱         | 類型 | 說明         | 範例 | 是否必須 |
| :----------- | :--- | :----------- | :--- | :------- |
| id           | int  | 課堂評量 ID  | 1    | O        |
| Bearer Token |      | 要為老師身分 |      | O        |

- 狀態說明
  課堂評量執行此 API 成功後狀態會更新為 collected

#### Response

-成功

- Body:

```json
{
  "result": true,
  "msg": ["Success"],
  "data": []
}
```

-失敗

#### 沒有權限(不是老師)

- Status: 403 Forbidden
- Body:

```json
{
  "result": false,
  "msg": ["You do not have permission to access this resource."]
}
```

#### MQTT

```json
{
  "course_data": "略",
  "status": "assessment_collected",
  "api": "",
  "method": "",
  "course_stu_ids": []
}
```

### course_assessments/{id}/actions/correct(POST)-檢討課堂評量

#### Request

- Method: **POST**
- URL: `course_assessments/{id}/actions/correct`
- Headers: Content-Type:multipart/form-data
- Path-params:

| 名稱         | 類型 | 說明         | 範例 | 是否必須 |
| :----------- | :--- | :----------- | :--- | :------- |
| id           | int  | 課堂評量 ID  | 1    | O        |
| Bearer Token |      | 要為老師身分 |      | O        |

- 狀態說明
  課堂評量執行此 API 成功後狀態會更新為 correcting

#### Response

-成功

- Body:

```json
{
  "result": true,
  "msg": ["Success"],
  "data": []
}
```

-失敗

#### 沒有權限(不是老師)

- Status: 403 Forbidden
- Body:

```json
{
  "result": false,
  "msg": ["You do not have permission to access this resource."]
}
```

#### MQTT

```json
{
  "course_data": "略",
  "status": "assessment_correcting",
  "api": "",
  "method": "",
  "course_stu_ids": []
}
```

### course_assessments/{id}/actions/publish_answer(POST)-老師公布課堂評量答案

#### Request

- Method: **POST**
- URL: `course_assessments/{id}/actions/publish_answer`
- Headers: Content-Type:multipart/form-data
- Path-params:

| 名稱             | 類型 | 說明             | 範例                    | 是否必須                        |
| :--------------- | :--- | :--------------- | :---------------------- | :------------------------------ |
| id               | int  | 課堂評量 ID      | 1                       | O                               |
| Bearer Token     |      | 要為老師身分     |                         | O                               |
| question_answers | json | 題目 ID 對應答案 | {"61":"ABC", "62":"BC"} | X                               |
| page_id          | int  | 頁數 ID          | 13                      | X(如果 correct_file 在的話必須) |
| correct_file     | file | 圖片             |                         | X                               |

- 範例 form fields

```
question_answers => {"62":"ABD", "65":"B"}
page_id => 13
correct_file => "answer.png"
```

- 狀態說明
  課堂評量執行此 API 成功後狀態會更新為 correcting

- 公布之後會自動計算所有題目學生的得分

#### Response

-成功

- Body:

```json
{
  "result": true,
  "msg": ["Success"],
  "data": []
}
```

-失敗

#### 沒有權限(不是老師)

- Status: 403 Forbidden
- Body:

```json
{
  "result": false,
  "msg": ["You do not have permission to access this resource."]
}
```

#### 題目 ID 錯誤

```json
{
  "result": false,
  "msg": ["Question id not found:19, 23"]
}
```

#### 答案選項格式錯誤 (EX:字母回答成數字)

```json
{
  "result": false,
  "msg": ["Answer option type error:19, 23"]
}
```

#### MQTT

```json
{
  "course_data": "略",
  "status": "assessment_corrected",
  "api": "",
  "method": "",
  "course_stu_ids": []
}
```

### course_assessments/{id}/actions/correct_hand_essay(POST)-老師批閱課堂評量手寫題&文字題

#### Request

- Method: **POST**
- URL: `course_assessments/{id}/actions/correct_hand_essay`
- Headers: Content-Type:multipart/form-data
- Path-params:

| 名稱          | 類型       | 說明         | 範例 | 是否必須 |
| :------------ | :--------- | :----------- | :--- | :------- |
| id            | int        | 課堂評量 ID  | 1    | O        |
| course_stu_id | int        | 課堂學生 ID  | 1    | O        |
| question_id   | int        | 評量問題 ID  | 1    | O        |
| correct_file  | image file | 批閱結果圖   |      | X        |
| score         | int        | 此題得分     | 5    | X        |
| Bearer Token  |            | 要為老師身分 |      | O        |

#### Response

-成功

- Body:

```json
{
  "result": true,
  "msg": ["Success"],
  "data": []
}
```

-失敗

#### 沒有權限(不是老師)

- Status: 403 Forbidden
- Body:

```json
{
  "result": false,
  "msg": ["You do not have permission to access this resource."]
}
```

#### 題目 ID 錯誤

```json
{
  "result": false,
  "msg": ["Question id not found:19, 23"]
}
```

#### MQTT

```json
{
  "course_data": "略",
  "status": "assessment_corrected",
  "api": "course_assessments/{id}/actions/get_correct",
  "method": "get",
  "parameter": "{course_stu_id}"
}
```

### course_assessments/{id}/actions/get_answering_status(GET)-取得課堂評量即時答題狀態

#### Request

- Method: **GET**
- URL: `course_assessments/{id}/actions/get_answering_status`
- Headers:
- Path-params:

| 名稱         | 類型 | 說明                    | 範例                                | 是否必須 |
| :----------- | :--- | :---------------------- | :---------------------------------- | :------- |
| id           | int  | 課堂評量 ID             | 1                                   | O        |
| Bearer Token |      | 有登入的學生/老師必須要 |                                     | X        |
| token        |      | 訪客學生必須要          | 10-d401f35993b3f038d24c552b9b3c3a53 | X        |

#### Response

- param:

| 名稱             | 類型 | 說明                 | 範例 |
| :--------------- | :--- | :------------------- | :--- |
| total_stu_count  | int  | 有參加評量的學生數   | 18   |
| finish_stu_count | int  | 評量已經交卷的學生數 | 8    |

-成功

- Body:

```json
{
  "result": true,
  "msg": ["Success"],
  "data": {
    "total_stu_count": 18,
    "finish_stu_count": 8
  }
}
```

### course_assessments/{id}/actions/get_statistics(GET)-取得課堂評量答題統計

#### Request

- Method: **GET**
- URL: `course_assessments/{id}/actions/get_statistics`
- Headers:
- Path-params:

| 名稱         | 類型 | 說明                    | 範例                                | 是否必須 |
| :----------- | :--- | :---------------------- | :---------------------------------- | :------- |
| id           | int  | 課堂評量 ID             | 1                                   | O        |
| Bearer Token |      | 有登入的學生/老師必須要 |                                     | X        |
| token        |      | 訪客學生必須要          | 10-d401f35993b3f038d24c552b9b3c3a53 | X        |

**status 為 running/closed/stopped 時不可使用**

#### Response

- param:

| 名稱             | 類型 | 說明                                                                         | 範例 |
| :--------------- | :--- | :--------------------------------------------------------------------------- | :--- |
| pages-statistics |      | 課堂評量頁面中回答結果統計(是非題,單選題,複選題)/學生回答內容(文字題,手寫題) |      |

- 是非題,單選題,複選題
  學生回答內容: 題目 ID 對應 {
  course_stus: array, 學生資料,
  answer: string, 學生回答 (是非包含 O,X,NO_ANS)
  result: integer, 比例(是非)/人數(單選,複選)
  }

- 文字題,手寫題
  學生回答內容: 題目 ID 對應 {
  course_stu: json, 學生資料,
  answer: string, 學生回答,
  score: integer, 學生得分
  }

-成功

- Body:
  因資料太多, page&statistics 只舉一個為例

```json (文字題)
{
  "result": true,
  "msg": ["Success"],
  "data": {
    "id": 2,
    "course_id": 1,
    "created_at": "2024-02-14 10:34:53",
    "updated_at": "2024-02-15 12:20:21",
    "deleted_at": null,
    "status": "correcting",
    "quest_type": "essay",
    "pages": [
      {
        "id": 7,
        "course_assessment_id": 2,
        "quest_number": 4,
        "page": 1,
        "quest_file_id": 94,
        "option_number": 0,
        "option_type": "",
        "score": 12,
        "created_at": "2024-02-15 10:05:06",
        "updated_at": "2024-02-15 10:05:06",
        "deleted_at": null,
        "options": [],
        "statistics": {
          "50": [
            {
              "course_stu": {
                "id": 4,
                "course_id": 1,
                "user_id": 0,
                "nickname": "小火",
                "is_visitor": 1,
                "score": 5,
                "avatar_file_id": 1,
                "is_online": 1,
                "created_at": "2023-12-30 11:39:56",
                "updated_at": "2023-12-30 11:39:56",
                "deleted_at": null,
                "stream_url": null,
                "comment": "",
                "avatar_file": {
                  "id": 1,
                  "uploader_id": 0,
                  "uploader_type": "student",
                  "file_type": "image",
                  "course_id": 1,
                  "drive_id": "GOMQXKw0NRF5CAq3HBOk7fx1cntuk1sxrirZDoCV.png",
                  "created_at": "2023-12-30 11:32:58",
                  "updated_at": "2023-12-30 11:32:58",
                  "deleted_at": null
                }
              },
              "answer": "ans1",
              "score": 0
            }
          ]
        },
        "questions": [
          {
            "id": 50,
            "page_id": 7,
            "answer": "ans1",
            "created_at": "2024-02-15 10:58:32",
            "updated_at": "2024-02-15 12:42:49",
            "deleted_at": null,
            "order": 1
          },
          {
            "id": 51,
            "page_id": 7,
            "answer": "ans2",
            "created_at": "2024-02-15 10:58:32",
            "updated_at": "2024-02-15 12:42:49",
            "deleted_at": null,
            "order": 2
          },
          {
            "id": 52,
            "page_id": 7,
            "answer": "ans33",
            "created_at": "2024-02-15 10:58:32",
            "updated_at": "2024-02-15 12:42:49",
            "deleted_at": null,
            "order": 3
          },
          {
            "id": 53,
            "page_id": 7,
            "answer": "ans44",
            "created_at": "2024-02-15 10:58:32",
            "updated_at": "2024-02-15 12:42:49",
            "deleted_at": null,
            "order": 4
          }
        ],
        "course_assessment": {
          "id": 2,
          "course_id": 1,
          "created_at": "2024-02-14 10:34:53",
          "updated_at": "2024-02-15 12:20:21",
          "deleted_at": null,
          "status": "correcting",
          "quest_type": "essay"
        }
      }
    ]
  }
}
```

```json (是非題, 單選題, 多選題)
{
  "result": true,
  "msg": ["Success"],
  "data": {
    "id": 4,
    "course_id": 1,
    "created_at": "2024-02-15 18:14:28",
    "updated_at": "2024-02-17 20:07:59",
    "deleted_at": null,
    "status": "collected",
    "quest_type": "tf/single/multiple",
    "pages": [
      {
        "id": 10,
        "course_assessment_id": 4,
        "quest_number": 2,
        "page": 1,
        "quest_file_id": 96,
        "option_number": 4,
        "option_type": "character",
        "score": 12,
        "created_at": "2024-02-15 18:15:56",
        "updated_at": "2024-02-15 18:15:56",
        "deleted_at": null,
        "options": ["A", "B", "C", "D"],
        "statistics": {
          "60": [
            {
              "course_stus": [
                {
                  "id": 4,
                  "course_id": 1,
                  "user_id": 0,
                  "nickname": "小火",
                  "is_visitor": 1,
                  "score": 5,
                  "avatar_file_id": 1,
                  "is_online": 1,
                  "created_at": "2023-12-30 11:39:56",
                  "updated_at": "2023-12-30 11:39:56",
                  "deleted_at": null,
                  "stream_url": null,
                  "comment": "",
                  "avatar_file": {
                    "id": 1,
                    "uploader_id": 0,
                    "uploader_type": "student",
                    "file_type": "image",
                    "course_id": 1,
                    "drive_id": "GOMQXKw0NRF5CAq3HBOk7fx1cntuk1sxrirZDoCV.png",
                    "created_at": "2023-12-30 11:32:58",
                    "updated_at": "2023-12-30 11:32:58",
                    "deleted_at": null
                  }
                },
                {
                  "id": 5,
                  "course_id": 1,
                  "user_id": 0,
                  "nickname": "小土",
                  "is_visitor": 1,
                  "score": 10,
                  "avatar_file_id": 1,
                  "is_online": 1,
                  "created_at": "2023-12-30 13:06:05",
                  "updated_at": "2024-01-19 11:17:15",
                  "deleted_at": null,
                  "stream_url": null,
                  "comment": "",
                  "avatar_file": {
                    "id": 1,
                    "uploader_id": 0,
                    "uploader_type": "student",
                    "file_type": "image",
                    "course_id": 1,
                    "drive_id": "GOMQXKw0NRF5CAq3HBOk7fx1cntuk1sxrirZDoCV.png",
                    "created_at": "2023-12-30 11:32:58",
                    "updated_at": "2023-12-30 11:32:58",
                    "deleted_at": null
                  }
                }
              ],
              "answer": "A",
              "result": 5
            }
          ]
        },
        "questions": [
          {
            "id": 56,
            "page_id": 10,
            "answer": "A",
            "created_at": "2024-02-15 18:16:45",
            "updated_at": "2024-02-17 20:08:56",
            "deleted_at": null,
            "order": 1
          },
          {
            "id": 57,
            "page_id": 10,
            "answer": "B",
            "created_at": "2024-02-15 18:16:45",
            "updated_at": "2024-02-17 20:08:56",
            "deleted_at": null,
            "order": 2
          }
        ],
        "course_assessment": {
          "id": 4,
          "course_id": 1,
          "created_at": "2024-02-15 18:14:28",
          "updated_at": "2024-02-17 20:07:59",
          "deleted_at": null,
          "status": "collected",
          "quest_type": "single"
        }
      }
    ]
  }
}
```

```json (手寫題)
{
  "result": true,
  "msg": ["Success"],
  "data": {
    "id": 7,
    "course_id": 1,
    "created_at": "2024-02-17 20:52:45",
    "updated_at": "2024-02-17 20:56:37",
    "deleted_at": null,
    "status": "correcting",
    "quest_type": "handwritten",
    "pages": [
      {
        "id": 16,
        "course_assessment_id": 7,
        "quest_number": 1,
        "page": 1,
        "quest_file_id": 102,
        "option_number": 0,
        "option_type": "",
        "score": 8,
        "created_at": "2024-02-17 20:53:48",
        "updated_at": "2024-02-17 20:53:48",
        "deleted_at": null,
        "options": [],
        "statistics": {
          "72": [
            {
              "course_stu": {
                "id": 4,
                "course_id": 1,
                "user_id": 0,
                "nickname": "小火",
                "is_visitor": 1,
                "score": 5,
                "avatar_file_id": 1,
                "is_online": 1,
                "created_at": "2023-12-30 11:39:56",
                "updated_at": "2023-12-30 11:39:56",
                "deleted_at": null,
                "stream_url": null,
                "comment": "",
                "avatar_file": {
                  "id": 1,
                  "uploader_id": 0,
                  "uploader_type": "student",
                  "file_type": "image",
                  "course_id": 1,
                  "drive_id": "GOMQXKw0NRF5CAq3HBOk7fx1cntuk1sxrirZDoCV.png",
                  "created_at": "2023-12-30 11:32:58",
                  "updated_at": "2023-12-30 11:32:58",
                  "deleted_at": null
                }
              },
              "answer_file": {
                "id": 97,
                "uploader_id": 2,
                "uploader_type": "teacher",
                "file_type": "image",
                "course_id": 1,
                "drive_id": "lapJ9ZHAcOXVhaeGxVgnn1Dm8W16NmvA4f0tBiHm.jpg",
                "created_at": "2024-02-15 18:16:18",
                "updated_at": "2024-02-15 18:16:18",
                "deleted_at": null
              },
              "correct_file": null,
              "score": null
            }
          ]
        },
        "questions": [
          {
            "id": 72,
            "page_id": 16,
            "answer": null,
            "created_at": "2024-02-17 20:54:13",
            "updated_at": "2024-02-17 20:54:13",
            "deleted_at": null,
            "order": 1
          }
        ],
        "course_assessment": {
          "id": 7,
          "course_id": 1,
          "created_at": "2024-02-17 20:52:45",
          "updated_at": "2024-02-17 20:56:37",
          "deleted_at": null,
          "status": "correcting",
          "quest_type": "handwritten"
        }
      }
    ]
  }
}
```

-失敗

#### 沒有權限

```json
{
  "result": false,
  "msg": ["You do not have permission to access this resource."]
}
```

#### 評量 status 是為下方其中之一['running', 'closed', 'stopped']

```json
{
  "result": false,
  "msg": ["The assessment cannot get statistics in current status."]
}
```

### course_assessments/{id}/actions/get_result(GET)-取得學生個人課堂評量結果

#### Request

- Method: **GET**
- URL: `course_assessments/{id}/actions/get_result`
- Headers:
- Path-params:

| 名稱         | 類型 | 說明           | 範例                                | 是否必須 |
| :----------- | :--- | :------------- | :---------------------------------- | :------- |
| id           | int  | 課堂評量 ID    | 1                                   | O        |
| Bearer Token |      | 有登入的學生   |                                     | X        |
| token        |      | 訪客學生必須要 | 10-d401f35993b3f038d24c552b9b3c3a53 | X        |

#### Response

-成功

- Body:
  PDF File

-失敗

#### 沒有權限

```json
{
  "result": false,
  "msg": ["You do not have permission to access this resource."]
}
```

### course_assessments/{id}/actions/get_stu_status(GET)-取得學生個人課堂評量狀態

#### Request

- Method: **GET**
- URL: `course_assessments/{id}/actions/get_stu_status`
- Headers:
- Path-params:

| 名稱         | 類型 | 說明           | 範例                                | 是否必須 |
| :----------- | :--- | :------------- | :---------------------------------- | :------- |
| id           | int  | 課堂評量 ID    | 1                                   | O        |
| Bearer Token |      | 有登入的學生   |                                     | X        |
| token        |      | 訪客學生必須要 | 10-d401f35993b3f038d24c552b9b3c3a53 | X        |

- return-params:

| 名稱   | 類型  | 說明                                        | 範例        |
| :----- | :---- | :------------------------------------------ | :---------- |
| data   | int   | 如 api 是 get 類型，會先傳該 api 回覆的資料 |             |
| status | int   | 除了狀態包含 MQTT 發送的狀態之外            | task_closed |
| api    | int   | api 路徑                                    |             |
| method | array | api 方法                                    |             |

- [回傳內容說明參考](#課堂評量學生取得個人化狀態)

#### Response

-成功

- Body:

```json
{
  "result": true,
  "msg": ["Success"],
  "data": [],
  "status": "assessment_answered",
  "api": "",
  "method": "",
  "parameter": []
}
```

-失敗

#### 沒有權限

```json
{
  "result": false,
  "msg": ["You do not have permission to access this resource."]
}
```

### course_assessments/{id}/actions/export(POST)-匯出課堂評量

#### Request

- Method: **POST**
- URL: `course_assessments/{id}/actions/export`
- Headers: Content-Type:multipart/form-data
- Path-params:

| 名稱         | 類型 | 說明         | 範例 | 是否必須 |
| :----------- | :--- | :----------- | :--- | :------- |
| id           | int  | 課堂評量 ID  | 1    | O        |
| Bearer Token |      | 要為老師身分 |      | O        |

#### Response

-成功

- Body:

```json
{
  "result": true,
  "msg": ["Success"],
  "data": []
}
```

-失敗

#### 沒有權限(不是老師)

- Status: 403 Forbidden
- Body:

```json
{
  "result": false,
  "msg": ["You do not have permission to access this resource."]
}
```

### course_assessments/{id}/actions/import(POST)-匯入課堂評量

#### Request

- Method: **POST**
- URL: `course_assessments/{id}/actions/import`
- Headers: Content-Type:multipart/form-data
- Path-params:

| 名稱         | 類型 | 說明         | 範例 | 是否必須 |
| :----------- | :--- | :----------- | :--- | :------- |
| id           | int  | 課堂評量 ID  | 1    | O        |
| Bearer Token |      | 要為老師身分 |      | O        |

- 回傳 id 為新建立的課堂評量 id, 評量狀態會是 closed

#### Response

-成功

- Body:

```json
{
  "result": true,
  "msg": ["Success"],
  "data": {
    "id": 11
  }
}
```

-失敗

#### 沒有權限(不是老師)

- Status: 403 Forbidden
- Body:

```json
{
  "result": false,
  "msg": ["You do not have permission to access this resource."]
}
```

### course_assessments/{id}/actions/remove(POST)-移除題庫課堂評量

#### Request

- Method: **POST**
- URL: `course_assessments/{id}/actions/remove`
- Headers: Content-Type:multipart/form-data
- Path-params:

| 名稱         | 類型 | 說明         | 範例 | 是否必須 |
| :----------- | :--- | :----------- | :--- | :------- |
| id           | int  | 課堂評量 ID  | 1    | O        |
| Bearer Token |      | 要為老師身分 |      | O        |

#### Response

-成功

- Body:

```json
{
  "result": true,
  "msg": ["Success"],
  "data": []
}
```

-失敗

#### 沒有權限(不是老師)

- Status: 403 Forbidden
- Body:

```json
{
  "result": false,
  "msg": ["You do not have permission to access this resource."]
}
```

### course_assessments/show_tpps(POST)-取得題庫課堂評量

#### Request

- Method: **GET**
- URL: `course_assessments/show_tpps`
- Headers:
- Path-params:

| 名稱         | 類型 | 說明         | 範例 | 是否必須 |
| :----------- | :--- | :----------- | :--- | :------- |
| Bearer Token |      | 要為老師身分 |      | O        |

#### Response

-成功

- Body:

```json
{
  "result": true,
  "msg": ["Success"],
  "data": [
    {
      "id": 6,
      "course_id": 1,
      "created_at": "2024-02-17 20:43:23",
      "updated_at": "2024-02-17 20:47:17",
      "deleted_at": null,
      "status": "correcting",
      "quest_type": "tf",
      "pages": [
        {
          "id": 14,
          "course_assessment_id": 6,
          "quest_number": 2,
          "page": 1,
          "quest_file_id": 100,
          "option_number": 0,
          "option_type": "tf",
          "score": 8,
          "created_at": "2024-02-17 20:43:41",
          "updated_at": "2024-02-17 20:43:41",
          "deleted_at": null,
          "options": ["O", "X"],
          "question_ids": [68, 69],
          "quest_file": {
            "id": 100,
            "uploader_id": 2,
            "uploader_type": "teacher",
            "file_type": "image",
            "course_id": 1,
            "drive_id": "OqQEYrnoJnKYs8ReGHMgHlPp0NZ58qg6p12NtUsD.jpg",
            "created_at": "2024-02-17 20:43:41",
            "updated_at": "2024-02-17 20:43:41",
            "deleted_at": null
          },
          "questions": [
            {
              "id": 68,
              "page_id": 14,
              "answer": "O",
              "created_at": "2024-02-17 20:43:55",
              "updated_at": "2024-02-17 20:47:22",
              "deleted_at": null,
              "order": 1
            },
            {
              "id": 69,
              "page_id": 14,
              "answer": "X",
              "created_at": "2024-02-17 20:43:55",
              "updated_at": "2024-02-17 20:47:22",
              "deleted_at": null,
              "order": 2
            }
          ]
        },
        {
          "id": 15,
          "course_assessment_id": 6,
          "quest_number": 2,
          "page": 2,
          "quest_file_id": 101,
          "option_number": 0,
          "option_type": "tf",
          "score": 8,
          "created_at": "2024-02-17 20:43:46",
          "updated_at": "2024-02-17 20:43:46",
          "deleted_at": null,
          "options": ["O", "X"],
          "question_ids": [70, 71],
          "quest_file": {
            "id": 101,
            "uploader_id": 2,
            "uploader_type": "teacher",
            "file_type": "image",
            "course_id": 1,
            "drive_id": "6uvlj08I0o3M1swuztExr43qRAdbGQK73uAVCbYW.jpg",
            "created_at": "2024-02-17 20:43:46",
            "updated_at": "2024-02-17 20:43:46",
            "deleted_at": null
          },
          "questions": [
            {
              "id": 70,
              "page_id": 15,
              "answer": "O",
              "created_at": "2024-02-17 20:43:55",
              "updated_at": "2024-02-17 20:47:22",
              "deleted_at": null,
              "order": 1
            },
            {
              "id": 71,
              "page_id": 15,
              "answer": "X",
              "created_at": "2024-02-17 20:43:55",
              "updated_at": "2024-02-17 20:47:22",
              "deleted_at": null,
              "order": 2
            }
          ]
        }
      ]
    },
    {
      "id": 5,
      "course_id": 1,
      "created_at": "2024-02-17 20:23:01",
      "updated_at": "2024-02-17 20:43:51",
      "deleted_at": null,
      "status": "correcting",
      "quest_type": "multiple",
      "pages": [
        {
          "id": 12,
          "course_assessment_id": 5,
          "quest_number": 2,
          "page": 2,
          "quest_file_id": 98,
          "option_number": 4,
          "option_type": "character",
          "score": 6,
          "created_at": "2024-02-17 20:23:46",
          "updated_at": "2024-02-17 20:23:46",
          "deleted_at": null,
          "options": ["A", "B", "C", "D"],
          "question_ids": [60, 61, 64, 65],
          "quest_file": {
            "id": 98,
            "uploader_id": 2,
            "uploader_type": "teacher",
            "file_type": "image",
            "course_id": 1,
            "drive_id": "g3A4h205CvUjUBuuWhQgkN4sUtpYXpPkPHeHH42w.jpg",
            "created_at": "2024-02-17 20:23:46",
            "updated_at": "2024-02-17 20:23:46",
            "deleted_at": null
          },
          "questions": [
            {
              "id": 60,
              "page_id": 12,
              "answer": "ABC",
              "created_at": "2024-02-17 20:24:27",
              "updated_at": "2024-02-17 20:34:20",
              "deleted_at": null,
              "order": 1
            },
            {
              "id": 61,
              "page_id": 12,
              "answer": "BD",
              "created_at": "2024-02-17 20:24:28",
              "updated_at": "2024-02-17 20:34:20",
              "deleted_at": null,
              "order": 2
            },
            {
              "id": 64,
              "page_id": 12,
              "answer": null,
              "created_at": "2024-02-17 20:43:51",
              "updated_at": "2024-02-17 20:43:51",
              "deleted_at": null,
              "order": 1
            },
            {
              "id": 65,
              "page_id": 12,
              "answer": null,
              "created_at": "2024-02-17 20:43:51",
              "updated_at": "2024-02-17 20:43:51",
              "deleted_at": null,
              "order": 2
            }
          ]
        },
        {
          "id": 13,
          "course_assessment_id": 5,
          "quest_number": 2,
          "page": 1,
          "quest_file_id": 99,
          "option_number": 4,
          "option_type": "character",
          "score": 8,
          "created_at": "2024-02-17 20:23:59",
          "updated_at": "2024-02-17 20:23:59",
          "deleted_at": null,
          "options": ["A", "B", "C", "D"],
          "question_ids": [62, 63, 66, 67],
          "quest_file": {
            "id": 99,
            "uploader_id": 2,
            "uploader_type": "teacher",
            "file_type": "image",
            "course_id": 1,
            "drive_id": "1d7t9MYxYaAyhPSMhctMIM8s5atqBuYm1TyVAjgR.jpg",
            "created_at": "2024-02-17 20:23:59",
            "updated_at": "2024-02-17 20:23:59",
            "deleted_at": null
          },
          "questions": [
            {
              "id": 62,
              "page_id": 13,
              "answer": "BD",
              "created_at": "2024-02-17 20:24:28",
              "updated_at": "2024-02-17 20:34:20",
              "deleted_at": null,
              "order": 1
            },
            {
              "id": 63,
              "page_id": 13,
              "answer": "AC",
              "created_at": "2024-02-17 20:24:28",
              "updated_at": "2024-02-17 20:34:20",
              "deleted_at": null,
              "order": 2
            },
            {
              "id": 66,
              "page_id": 13,
              "answer": null,
              "created_at": "2024-02-17 20:43:51",
              "updated_at": "2024-02-17 20:43:51",
              "deleted_at": null,
              "order": 1
            },
            {
              "id": 67,
              "page_id": 13,
              "answer": null,
              "created_at": "2024-02-17 20:43:51",
              "updated_at": "2024-02-17 20:43:51",
              "deleted_at": null,
              "order": 2
            }
          ]
        }
      ]
    }
  ]
}
```

-失敗

#### 沒有權限(不是老師)

- Status: 403 Forbidden
- Body:

```json
{
  "result": false,
  "msg": ["You do not have permission to access this resource."]
}
```
