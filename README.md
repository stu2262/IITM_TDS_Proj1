- **Data** **Extraction**: A PyScript used the requests library to extract data via the search HTML parameter, preprocess it, and create a CSV file. Repositories’ details were then extracted using the repo parameter and user logins, appending results to another CSV file.
- **Most Interesting Fact**: waferbaby is a story teller masquerading like a programmer: They created a website that's just a collection of what people do and what they use for it! It's a veritable goldmine of data that would be extremely useful but it's also so many stories hidden away. I wonder how many such diamonds of users/repos are there in the dirt.
- **Recommendation**: Followers, and the closely related connections, depend primarily on what you work on: Target programs/repos that will be used by a lot of programmers, and/or ideas that are extremely unique and kindof helpful (even if niche), like the aforementioned example of waferbaby. 


# Data Extraction Deets:

Well, I was apparently one of the two people in the world who has been publicly coding for a while, but never used Github. So naturally, I have no idea how Github works, let alone its API. 

So where do I start but the API docs, apprehensive about how complex it will be (especially reading about a GitHub CLI, and me thinking it was a new language and not realizing CLI was just Command Line Interface). My luck, I came to realize most of the API calls could be managed with just some HTML requests and a personal API key. 

So I create my API key, and code up a tiny script in python to get the data of all users in Sydney (with some help from some AI). I start manipulating them, filtering them (by number of followers), converting the data into the required form, etc. when I came to realize the size of my list was exactly 1000. 
That seemed suspiciously exact, and I decided to do a general search on GitHub directly, and the number of users in Sydney skyrocketed to 34.9k + results. And after a little exploring, I realized that the number of users displayed/sent to an upi is limited to 1000, hence why I got this limited list.

So I changed my get command to also filter for followers>100, and this time it worked in extracting the required users (332).

Now, I get the required information from each user's url, and append it into a list after the required pre-processing (whitespaces, bools, etc). I append it into a list of lists with which I then create the users.csv file. 

---

Now, onto the repositories part. I first started off with a rough ballpark of how many calls I might have to make by seeing the sum of repos columns: Approximately 29k+ repos. Herein comes my complete misunderstanding of github api responses: I spent hours freaking out that I had to make 29K calls, which would take the better part of 6 hours given GitHub’s 5k/hr api call limit. (I did not realize all this data of a user (or atleast 100 repos’ data) will come with the single api call of …/user/repos.)

After realizing that, and having a mini-celebration for not having to make api calls for 6 hrs, I whip up a script to take the required repo-information and append it to a csv file. Of course I wrote some code to check for the 500 repos limit, along with other relevant processing, and I finally got a file with just over 28K rows.

---

Once all this is done, I finally begin analyzing the data.

# Analysis

Analysis on this data, especially for the questions, was done using simple pyscripts with pandas, with some of the easier questions being done in spreadsheets itself. Further analysis of the data was done using some basic statistical tools like correlation and regression.

Finally, direct analysis was done manually. This was done primarily by reading the bios, checking number of repos/followers, and investigating repos for any pattern and/or uniqueness found, which lead to my aforementioned fact about waferbaby.
