Test Github merge queues
========================

Dummy repo that has a long running CI job and release-please enabled to test Github merge queues.

Things that can be tested:
- Submit 2 PRs, wait for all checks to pass, then merge them one after the other. You'll see the merge queue will process them one by one
- Submit at least one PR with either `feat` of `fix` so that release-please submit its own PR. Merge release-please PR and wait for the merge queue to process it. Everything should be as before
- Try merging both a user PR and release-please PR, in that order or in the reverse order

Guillaume's experiment results:

Merge queues works as expected. I tried the things outlined above, and the only thing to notice is that whe you merge a release-please PR on a non-empty merge queue, the PRs currently being process in the merge queue won't appear in the CHANGELOG.
This is kind-of expected b/c release-please won't be able to update the current release PR as it has already been submitted to the merge queue.

An easy workaround for this is I think to make the release-please PR jump the queue when it's being added to the queue. This way, it will be merged first and the following PRs will be added to the next release changelog. However, this is not something that seems easy to automate right now, the only seems to be to have a human click on this "jump queue" button. 

If the human cutting the release forgets to click that button, the CHANGELOG will be incomplete, which is not great, but also not the end of the world given that it can be post edited.
