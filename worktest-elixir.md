# Work test
In this test, we want to see how you would write a feed consumer in
elixir, it should fetch odds from a feed on S3. Its task will be to
find pre-match odds for matches and store them with our id as JSON.

One file per match one way could be `our_id.json` (ex: 123445.json), A
Bonus points if stored on s3.  Ensure that you only use complete odds
(1, x and 2), and include their match id in the output.

Example output: `123445.json`

    {
      id: 4321,
      home: "Home name",
      away: "Away name",
      outcomes: {
        "1": "2.44",
        "x": "3.33",
        "2:" "4.44"
      }
    }

A high level view of the algorithm would be:
- Consume odds feed
- Find relevant matches, that contain all outcomes.
- Ensure that that match is in the match schedule.
- Write the result to disk/s3.

Things to consider/discuss:
- How would you structure this project to support multiple feeds of different formats?
- What issues would you see arising with collecting odds from a feed similar to this?
- When would you consider match odds invalid? And how would you keep track of this?
- What to do if the feed and match schedule's team names differ, how
  could you get a good matching with some fuzziness?

## Match schedule

`http://Tengu:Sciopod@test.footballaddicts.com/test_assignment/match_schedule?last_checked_at=[UNIX_TIMESTAMP]`
Used for mapping our feed, do use `last_checked_at` to ensure that you
do not request data to often (this should not be polled more than once
per hour).

## Odds Feed

`https://s3-eu-west-1.amazonaws.com/fa-oddball/worktest/ag.json`
This feed simulates a feed from an odds provider, so it might do some
unexpected things. This feed is refreshed once a minute.
