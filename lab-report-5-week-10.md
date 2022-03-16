# Lab Report 5
## Finding tests with different results
To find the tests with different results my group made the directories, my_week10 and week10. In my_week10, I used `git clone` to copy my markdown-parse repo in it. I then put in put Professor Politz's markdown-parse repo. Then I copied `test-files` folder with all of the test files into my_week10 using `cp -r week10.txt ~/my_week10/markdown-parse/test-files` in my_week10.

I added bash scripts to both my_week10 and week10 directories to print out the respective file and their outputs. 

Then I ran `diff ~/week10/markdown-parse/week10.txt ~/my_week10/markdown-parse/my_results.txt > differences.txt` to get a text file with the differences between the two output files. I also used `vimdiff ~/week10/markdown-parse/week10.txt ~/my_week10/markdown-parse/my_results.txt` to get a view of the differences. 
