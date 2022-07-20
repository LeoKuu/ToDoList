# Todolist

### clone repository 後於 ToDoList 資料夾使用 command line 輸入

```
1. npm install
```
```
2. npm run serve
```

### 指令輸入完成後即可出現畫面

![image](https://github.com/LeoKuu/ToDoList/blob/main/todolist.png)

說明 : [程式碼位置](https://github.com/LeoKuu/ToDoList/blob/main/src/components/ToDoList.vue)
   
   1. 在準備要做的任務欄位輸入完成後，點擊新增或 enter 觸發 addToDo 方法新增待辦事項。
   2. 狀態欄位預設為全部，利用 toDoFilter 方法判定待辦事項之狀態。
   3. 點擊待辦事項後觸發 changeComplated 方法，使該欄位狀態變為已完成且新增刪除線。
   4. 點擊待辦事項右方 X 後觸發 removeToDo 方法移除該待辦事項。
   5. 點擊右下方清除所有任務後觸發 cleanToDo 方法移除所有待辦事項。
   6. toDoLength 方法計算未完成任務之筆數 
