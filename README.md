- **Data** **Extraction**: A PyScript used the requests library to extract data via the search HTML parameter, preprocess it, and create a CSV file. Repositories’ details were then extracted using the repo parameter and user logins, appending results to another CSV file.
- **Most Interesting Fact**: 
- **Recommendation**:


# Data Extraction Deets:

Well, I was apparently one of the two people in the world who has been publicly coding for a while, but never used Github. So naturally, I have no idea how Github works, let alone its API. 

So where do I start but the API docs, apprehensive about how complex it will be (especially reading about a GitHub CLI, and me thinking it was a new language and not realizing CLI was just Command Line Interface). My luck, I came to realize most of the API calls could be managed with just some HTML requests and a personal API key. 

So I create my API key, and code up a tiny script in python to get the data of all users in Sydney (with some help from some AI). I start manipulating them, filtering them (by number of followers), converting the data into the required form, etc. when I came to realize the size of my list was exactly 1000. 
That seemed suspiciously exact, and I decided to do a general search on GitHub directly, and the number of users in Sydney skyrocketed to 34.9k + results. And after a little exploring, I realized that the number of users displayed/sent to an upi is limited to 1000, hence why I got this limited list.

So I changed my get command to also filter for followers>100, and this time it worked in extracting the required users (371).

Now, I get the required information from each user's url, and append it into a list after the required pre-processing (whitespaces, bools, etc). I append it into a list of lists with which I then create the users.csv file. 

---

Now, onto the repositories part. I first started off with a rough ballpark of how many calls I might have to make by seeing the sum of repos columns: Approximately 46k+ repos. Herein comes my complete misunderstanding of github api responses: I spent hours freaking out that I had to make 46k calls, which would take the better part of 10 hours given GitHub’s 5k/hr api call limit. (I did not realize all this data of a user (or atleast 100 repos’ data) will come with the single api call of …/user/repos.)

After realizing that, and having a mini-celebration for not having to make api calls for 10 hrs, I whip up a script to take the required repo-information and append it to a csv file. Of course I wrote some code to check for the 500 repos limit, along with other relevant processing, and I finally got a file with just over 32K rows.

Actually, my code breaks around user number 348, np1. I had written with the assumption that anyone with more than 100 followers would have atleast one repo, but apparently np1 had none.  This broke my code which called the first element of a list of nothing. 

[So backstory time, not relevant: np1 apparently was the biggest contributor to yewtube which allows people to watch youtube directly from the terminal, which is frankly very cool. I’m also pretty sure he created this repo, given his achievement of starstruck “@np1 created a repository that has many stars”, but for some reason it is showing he has 0 repositories. He prolly had transferred the ownership to someone else, as I found out he is also inactive for the past 8 years, with yewtube being his biggest project]

I do realize that this wasn’t a good assumption and luckily this had a real simple fix, a check, which I have now added to my code. [However, I did not rerun the code with the fix, instead opting for just running the code after np1 (a list of 20+ users), since I was close to the api limit for that hour.]

I had yet another heart attack when I saw I had 32K rows instead of 46k rows, but I remembered my 500 per user limit. Still, at a glance most people had like 50-300 repos, so this seemed a little high, so I did some basic analysis with excel and figured out the amount of repos is correct when I filter for this limit, and the discrepancy occurs because of some power users with thousands or repositories. 

[Premier among them being johndpope who has created 9000+ repos in 14 yrs. That’s over 2 a day! His current rate (56 in october) is showing that he has no intentions of stopping. As for why, I’m not entirely sure but his plethora of projects does show him to be someone who’d be coding and creating far more than the average coder.]

---

Once all this is done, I finally begin analyzing the data

