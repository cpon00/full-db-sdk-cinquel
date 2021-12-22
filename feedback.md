

## Cinquel

##### https://github.com/lmu-cmsi3520-fall2021/full-db-sdk-cinquel

| Category | Feedback | Points |
| --- | --- | ---: |
| _about.md_ | | |
| • Dataset link | Dataset link is provided in _about.md_ |  |
| • Dataset description | Dataset is described sufficiently | 5/5 |
| • Application description | The instructions for this were: “The application you have envisioned that uses this dataset: general description, prominent use cases (involving underlying data)” —as such, the headings weren’t quite the best fit (they might have been before but ideally they were reviewed in light of this final version); you mainly answered the use cases but did not describe a specific application that _you_ had  in mind for this SDK. It might seem trivial but actually having a clear notion of this helps you formulate better and more specific queries<br><br>In the end, you did describe a lot of fitting things that one can do, even if not under a single fully cohesive application idea. So this deduction is more about “align your response more closely to the information need of the instructions” (–1) | 4/5 |
| • Choice rationale | Database choice rationale effectively communicates reason for choosing a graph database model | 5/5 |
| • Choice assessment | Database choice assessment is expressed clearly—no wrong or right answer here of course, because it’s all about your view of the decision after the fact | 5/5 |
| _.gitignore_ | _.gitignore_ contains appropriate ignores |  |
| Schema | Schema is communicated clearly and according to the notation and naming conventions used by Neo4j | 10/10 |
| Preprocessing/loader | • _loader.py_ appears to run without issues<br><br>• Import appears to run without issues: `121071 nodes 284192 relationships 389847 properties` | 20/20 |
| Indexing | Indexing scheme is sufficiently implemented and documented with timing data; no _explanation_ data though—that would have definitively showed that the database is definitely using the index vs. a sequential scan (–3)<br><br>In addition, the _choice_ of index won’t bear out in production—the index is on movie title, which is unlikely to be searched on exactly. Searches by substring or regex do _not_ benefit from an index. Best to index other values that may be queried exactly or via simple < or ><br><br>Still, the speedup is apparent isn’t it, even if it’s only a matter of milliseconds 🚀 | 17/20 |
| _setup.md_ | _setup.md_ is accurate, complete, and clear; instructions and results went as documented<br><br>But watch your proofreading! There’s a non-trivial typo in the import command (`-nodes=Keywords=` should be `--nodes=Keyword=`). It’s always good to test-drive your documentation _as-is_ before closing it out (–1) | 9/10 |
| DAL module | | |
| • Configuration/setup | Configuration code uses library correctly and properly separates configuration information as an environment variable |  |
| • Featured queries | Featured queries successfully perform their intended queries and include the requested documentation. Quite a selection here—nicely done!<br><br>My only tweak is that some functions hold back by just returning a movie title (e.g., `get_actor_performances`, `get_movies_with_keyboard`)—may as well return the entire movie node there for graphability and use as a helper function (i.e., picking up the movie ID) (–1) | 19/20 |
| • CRUD + transaction | CRUD functions generally appear to work as expected and include the requested documentation, with the following caveats:<br><br>• `remove_movie` performs the deletion that it was intended to do…if there is a movie with the given ID. But there’s no way for the caller to know this. It should return something derived from the return value of `session.run` (–1). Because this is missing, the function caller has to take care of this—and it’s good that they do, thanks to you `does_id_exist` helper—but from a separation-of-concerns perspective, this capability is best handled as close to the database as possible<br><br>In the transaction department, you mark a function as needing a transaction but there is no actual transaction code given, whether a `BEGIN`/`COMMIT` pair or a call to `writeTransaction`. The operation is definitely complex enough to merit a transaction, so the deduction is lower than it would otherwise have been (–2) | 22/25 |
| • Helpers | `does_id_exist` is a great choice for a helper function (and even if `remove_movie` did return a value, it would still be helpful in other scenarios) plus other queries also return a movie ID somewhere in the results. Thus they can also play the role of helper functions in their own right<br><br>The functions also include the requested documentation ✅ | 15/15 |
| PoC | The command line suite appears to behave as expected for an application PoC—some little bugs found but otherwise gucci<br><br>• The choice to raise exceptions is generally sound, but for end-user programs you want to _handle_ them in a way that avoids technical output like stack traces. So argument checks or non-existent values as exceptions is fine, but make sure you have handlers that prevent the scary stack trace from appearing (–1)<br><br>• Some filenames (e.g., _get_rating.py_) or help messages/documentation (e.g., _acted_together.py_) aren’t fully consistent with each other. This is a lot to juggle so we’ll leave it be<br><br>Some great error-checking all around—nicely done! Just absorb the stack traces 🥶 | 19/20 |
| Retrospective | | |
| • _group-retrospective.md_ | _group-retrospective.md_ describes each group member’s role and the overall interaction vibe | 5/5 |
| • Individual email | Credit applied to those who sent an email | |
| Tutorial video | Relational theory concepts sufficiently touched on—“deer in headlights” largely averted 😁 Or should I say “reindeer in headlights” to match your theme better 🦌🛷<br><br>Ideally your examples would have actually used your dataset…it’s easy to walk through examples from other places but showing it from your own data adds a desirable dash of personalization | 30/30 |
| Code maintainability | No major code maintainability issues were found (that weren’t otherwise already pointed out) |  |
| Code readability | No major code readability issues were found (that weren’t otherwise already pointed out) |  |
| Version control | Not a lot of commits given the scope of this assignment, but with pretty descriptive messages; looks like more hands on the commit deck this time, with everyone having at least one…oh wait, except Carter. But I’m sure a part of him is in there somewhere |  |
| Punctuality | First commit on 12/2 7pm; last commit on 12/14 4:23pm |  |
| | **Total** | **185/195** |
