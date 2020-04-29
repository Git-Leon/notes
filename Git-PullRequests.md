* The image seen in this link :point_down:
  * https://files.slack.com/files-pri/T011D9JJPBQ-F012YHV3ML4/screen_shot_2020-04-29_at_2.32.03_pm.png
* signifies that the state of the branch with changes, and the branch to be merged into, are compatible in a way that there will be no subsequent merge conflicts.

* Upon merging `pull/1` with dev , the `pull/2` became out-of-synch with dev .
  * This means that the image seen in the link above, will not be available.
  * The merge button, will be replaced with something expressing that there are conflicts with the branch and the remote to be merged into.

* To be out-of-synch means that there are changes in pull/2 , that if merged into dev, would cause a conflict.
  * In this case, the conflict would be that the contents in pull/2 are from before pull/1  was merged with dev.
  * We call this state of data, _stale_.

* To resolve the staleness of pull/2, we synch it with dev by executing git pull origin dev , the git pushing whatever changes we receive.

* Finally, the merge button reappears on pull/2 .
  * We know that we can safely merge into dev  without conflicts arising.
