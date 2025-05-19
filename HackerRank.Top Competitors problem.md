Julia just finished conducting a coding contest, and she needs your help assembling the leaderboard!
Write a query to print the respective hacker_id and name of hackers who achieved full scores for more than one challenge.
Order your output in descending order by the total number of challenges in which the hacker earned a full score.
If more than one hacker received full scores in same number of challenges, then sort them by ascending hacker_id.

---

### Input Format

The following tables contain contest data:

* Hackers: The hacker_id is the id of the hacker, and name is the name of the hacker.

![1458526776-67667350b4-ScreenShot2016-03-21at7 45 59AM](https://github.com/user-attachments/assets/f01afb16-f153-442a-92c6-0e82f5010b39)

* Difficulty: The difficult_level is the level of difficulty of the challenge,
 and score is the maximum score that can be achieved for a challenge at that difficulty level.

![1458526915-57eb75d9a2-ScreenShot2016-03-21at7 46 09AM](https://github.com/user-attachments/assets/e39d759b-25c1-4844-b467-19d0c3abe11f)

* Challenges: The challenge_id is the id of the challenge, the hacker_id is the id of the hacker who created the challenge,
 and difficulty_level is the level of difficulty of the challenge.

![1458527032-f9ca650442-ScreenShot2016-03-21at7 46 17AM](https://github.com/user-attachments/assets/e99e472b-2411-4bf7-b583-9aca4929d1b1)

* Submissions: The submission_id is the id of the submission, hacker_id is the id of the hacker who made the submission,
 challenge_id is the id of the challenge that the submission belongs to, and score is the score of the submission.

![1458527077-298f8e922a-ScreenShot2016-03-21at7 46 29AM](https://github.com/user-attachments/assets/7378d8fe-3c5c-469a-9d8b-7bcc1b1f8ca8)

---

### Sample Input

Hackers Table:

![1458527241-6922b4ad87-ScreenShot2016-03-21at7 47 02AM](https://github.com/user-attachments/assets/f7b7d0d0-6d56-4e04-80f4-de7e068471cb)

Difficulty Table:

![1458527265-7ad6852a13-ScreenShot2016-03-21at7 46 50AM](https://github.com/user-attachments/assets/e7133309-41a7-478a-a384-647a5789d73b)

Challenges Table:

![1458527285-01e95eb6ec-ScreenShot2016-03-21at7 46 40AM](https://github.com/user-attachments/assets/36d929db-8380-4c1b-a28f-bc13411bddc3)

Submissions Table:

![1458527812-479a74b99f-ScreenShot2016-03-21at8 06 05AM](https://github.com/user-attachments/assets/cbde8bad-e25b-46ab-a69a-b845c192bc4f)

### Sample Output

``` {text}
90411 Joe
```

### Explanation


Hacker 86870 got a score of 30 for challenge 71055 with a difficulty level of 2, so 86870 earned a full score for this challenge.

Hacker 90411 got a score of 30 for challenge 71055 with a difficulty level of 2, so 90411 earned a full score for this challenge.

Hacker 90411 got a score of 100 for challenge 66730 with a difficulty level of 6, so 90411 earned a full score for this challenge.

Only hacker 90411 managed to earn a full score for more than one challenge, so we print the their hacker_id and name as 2 space-separated values.

--- 


## Query
``` sql
select h.hacker_id , h.name
from Hackers as h
join Submissions as s on s.hacker_id = h.hacker_id
join Challenges as c on c.challenge_id = s.challenge_id
join Difficulty as d on c.difficulty_level = d.difficulty_level
where d.score = s.score
group by h.hacker_id, h.name
having count(*) > 1
order by count(*) desc , h.hacker_id asc;
```





