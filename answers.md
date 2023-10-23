# Quiz questions

This is only a "quiz" in the loosest sense that it's asking questions whose
answers will be part of your grade. Please use *any resources you want*, as
long as you list those resources (e.g. peers, websites, etc.)

## Navigating logs

1. What is the SHA for the last commit made by Prof. Xanda on the branch
xanda_0000_movie_processing?
(For this and future questions, the first 5 characters is plenty - neither
Git nor I need the whole SHA.)
9b257

2. What is the SHA for the last commit associated with line 9 of this file?
b2ed39de


3. What did line 12 of this file say in commit d1d83?
I should really finish writing this.

4. What changed between commit e474c and 82045?
diff --git a/process_movie_data.py b/process_movie_data.py
index 71f23e1..13b0caa 100644
--- a/process_movie_data.py
+++ b/process_movie_data.py
@@ -15,9 +15,9 @@ def find_top_5(filename):
         rows = [r for r in csvr]
     
     # Sort data and get top 5
-    gross_sort = lambda x : x["Gross"]
+    gross_sort = lambda x : int(x["Gross"])
     rows.sort(key=gross_sort)
-    top_five = rows[:-5:-1]
+    top_five = rows[:-6:-1]
 
# Print out results
     for row in top_five:
(base) daisyabbott@MacBook-Pro-593 GitLab % 
ANSWER: 
It looks like gross was cast as an int, and the slicing was changed from -5 to 6, which means the criteria for the top movies was adjusted from excluding the last 5 elements to excluding the last 6 elements in the sorted list

## Predicting merges

Assume at the start of each of these three questions that your
branch for switching to a top-10 list was called `top_ten`
and your branch generalizing to any number of movies was called `top_N`.
Predict the behavior of these three possible operations - you don't
have to provide a full `diff` but you should describe at a high level
what changes would happen.

These questions are supposed to be separate paths, not cumulative;
for example, you should *not* assume that the operations of 5 were run
before 6. When testing outcomes later in the lab, you should make sure to
revert back to the state of the branch before you started these questions.

5. What do you think would happen if you ran the following commands?
What branches would change, and how?
```
git checkout test
git merge top_N
```
I think I may have messed up the git push directly before this and pushed to just top_N instead of test, but then modified for test and pushed for test, so it didn't work exactly as anticipated. I didn't end up runnin into a merge conflict for question 5. I recieved this message after running those ^ commands: Merge made by the 'ort' strategy.

6. What do you think would happen if you ran the following commands?
What branches would change, and how?
```
git checkout top_ten
git merge test
```
Upon running these commands, I ran into a merge conflict: Merge conflict in process_movie_data.py
Automatic merge failed; fix conflicts and then commit the result.
Which I suppose is to be expected? 

7. What do you think would happen if you ran the following commands?
What branches would change, and how?
```
git checkout test
git rebase top_ten
git rebase top_N
```
After running git rebase top_ten: dropping 21ea492722568aeea561deb6d45e2398e7ff5c44 updated to find_top_n function -- patch contents already upstream
Successfully rebased and updated refs/heads/test.

And after running git rebase top_N: warning: skipped previously applied commit 3f84e1c
hint: use --reapply-cherry-picks to include skipped commits
hint: Disable this message with "git config advice.skippedCherryPicks false"
Successfully rebased and updated refs/heads/test.

I did run into some major merge conflicts and had to handle it:
git pull --rebase origin test   
And am hoping I didn't mess this up too bad.