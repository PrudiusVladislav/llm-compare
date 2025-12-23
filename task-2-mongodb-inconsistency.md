# MongoDB data inconsisency
This is a prompt for solving the Task 2 - case of a data inconsistency issue in a MongoDB, that caused an unexpected bug on production.
The prompt:

```
Got this error in prod just now:

[15:18:18.852] WARN: handleTaskAnswer: Task not accessible 
{"app":"server","userId":"xxxxxxxxxxxxxxxxxxxxxxxx","subjectId":"xxxxxxxx","taskId":"67f67101bf5615c754e4bd2a","lessonId":"67f67101bf5615c754e4bd1d"}
[15:18:18.853] ERROR: /student/task/handle-answer 68a9797066da11d2e9e13ad1 "task_not_accessible" {"app":"server"}

Student is trying to answer a task but gets "task_not_accessible". The weird part is - the task shows up in the lesson on the frontend, user can see it. But when they try to submit an answer it fails.

I checked and the taskId 67f67101bf5615c754e4bd2a definitely exists in `tasksStatic` collection. The lessonId exists too. User has access to the course/lesson.

Here's the task doc from mongo:

{
  "_id": ObjectId("67f67101bf5615c754e4bd2a"),
  "courseId": ObjectId("6853c08708d0270a7f5f339a"),
  "lessonId": ObjectId("67f67101bf5615c754e4bd1d"),
  "key": [[]],
  ...other keys
  "descendants": [
    { "subjectId": "xxxxxx", "courseId": ObjectId("67f67100bf5615c754e4bcb9"), "taskId": ObjectId("67f67101bf5615c754e4bd2a") },
    { "subjectId": "xxxxxx", "courseId": ObjectId("6852d9392f27e2b918de3624"), "taskId": ObjectId("6852d9392f27e2b918de3695") }
  ]
}

Can you figure out why this is happening? The error gets thrown in handleTaskAnswer in student-service.js when the aggregation returns nothing. But the task is there so something in the pipeline must be filtering it out...

Find the root cause andp provide a fix.

```
