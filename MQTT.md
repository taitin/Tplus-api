### 課堂快問快答-MQTT/取得學生個人化狀態說明

#### 課堂快問快答學生取得個人化狀態

| 時機說明                 | status         | api                                       | method | 課堂快問快答 is_active |
| :----------------------- | :------------- | :---------------------------------------- | :----- | :--------------------- |
| 快問快答未開始/已結束    | quiz_closed    |                                           |        | 0                      |
| 學生還沒回答             | quiz_answering | `course_quizzes/{id}/actions/answer `     | post   | 1                      |
| 學生已回答               | quiz_answered  |                                           |        | 1                      |
| 快問快答已被老師批改完成 | quiz_corrected | `course_quizzes/{id}/actions/get_correct` | get    | 1      


### 課堂評量-MQTT/取得學生個人化狀態說明

#### 課堂評量學生取得個人化狀態

| 時機說明                 | status                | api                                          | method | 課堂評量 status |
| :----------------------- | :-------------------- | :------------------------------------------- | :----- | :-------------- |
| 評量未開始               | assessment_closed     |                                              |        | closed          |
| 評量答題中, 學生還沒回答 | assessment_answering  | `course_assessments/{id}/actions/answer `    | post   | running         |
| 評量答題中, 學生已回答   | assessment_answered   |                                              |        | running         |
| 評量被中止               | assessment_stopped    |                                              |        | stopped         |
| 評量已收卷               | assessment_collected  |                                              |        | collected       |
| 評量檢討中               | assessment_correcting |                                              |        | correcting      |
| 評量檢討完               | assessment_corrected  | `course_assessments/{id}/actions/get_result` |        | corrected       |




### 課堂搶答-MQTT/取得學生個人化狀態說明

#### 課堂搶答學生取得個人化狀態

| 時機說明                                | status              | api                                  | method | 課堂搶答 status |
| :-------------------------------------- | :------------------ | :----------------------------------- | :----- | :-------------- |
| 搶答未開始                              | qa_closed           |                                      |        | closed          |
| (加分)還沒人搶答成功/(競賽)學生還沒回答 | qa_answering        | `course_qas/{id}/actions/answer `    | post   | running         |
| (競賽)學生已回答                        | qa_answered         |                                      |        | running         |
| (加分)已有人成功搶答                    | qa_answered_success | `course_qas/{id}/actions/get_result` | get    | answered        |
| 搶答被中止                              | qa_stopped          |                                      |        | stopped         |
| 搶答時間到                              | qa_time_up          |                                      |        | time_up         |
| 搶答已完成                              | qa_complete         | `course_qas/{id}/actions/get_result` | get    | complete        |
