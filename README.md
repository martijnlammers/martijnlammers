### Hi there 👋

name: Update AoC Badges
on:
  schedule:                                      # run workflow based on schedule
    - cron: '6 5 1-25 12 *'                      # from the 1. December till 25. December every day at 5:06am (avoid load at full hours)
    
  workflow_dispatch:                             # allow to manually start the workflow 
  
# push:                                          # (disabled) run on push, be carefull with this setting 
                                                 # as the workflow should only be triggered at a rate lower than
                                                 # 4 times a hour to keep traffic on aoc site low 
jobs:
  update:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2                # clones your repo
          
      - uses: joblo2213/aoc-badges-action@v3
        with:
          userid: 00000                          # your user id, see setup on how to obtain
          session: ${{ secrets.AOC_SESSION }}    # secret containing session code, see setup on how to obtain
          
#         Optional inputs:
#         
#         year: 2021                                                                                     # The year for which stats should be retrieved
#         leaderboard: 'https://adventofcode.com/2020/leaderboard/private/view/00000.json'               # The url of the leaderboard from witch the data is fetched. Typically your private leaderboard.
#         file: 'README.md'                                                                              # The file that contains the badges
#         dayRegex: '(?<=https:\/\/img\.shields\.io\/badge\/day%20📅-)[0-9]+(?=-blue)'                   # Regular expression that finds the content of the day badge in your file.
#         starsRegex: '(?<=https:\/\/img\.shields\.io\/badge\/stars%20⭐-)[0-9]+(?=-yellow)'             # Regular expression that finds the content of the stars badge in your file.
#         daysCompletedRegex: '(?<=https:\/\/img\.shields\.io\/badge\/days%20completed-)[0-9]+(?=-red)'  # Regular expression that finds the content of the days completed badge iun your file.

      - uses: stefanzweifel/git-auto-commit-action@v4     # Step that pushes these local changes back to your github repo
        with:
          commit_message: Update badges
          file_pattern: README.md
<!--
**martijnlammers/martijnlammers** is a ✨ _special_ ✨ repository because its `README.md` (this file) appears on your GitHub profile.

Here are some ideas to get you started:

- 🔭 I’m currently working on ...
- 🌱 I’m currently learning ...
- 👯 I’m looking to collaborate on ...
- 🤔 I’m looking for help with ...
- 💬 Ask me about ...
- 📫 How to reach me: ...
- 😄 Pronouns: ...
- ⚡ Fun fact: ...
-->
