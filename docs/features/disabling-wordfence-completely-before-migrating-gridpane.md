# Disabling Wordfence completely before migrating | GridPane

# Disabling Wordfence completely before migrating

 

1 min read 

Wordfence is a popular security plugin, but it’s also been known to prevent migrations from completing successfully.

If you have Wordfence activated on the website that you’re migrating over to GridPane, we recommend that you disable it before making your export to ensure it doesn’t interfere.

Additionally, Wordfence often adds a hardcoded path to the .user.ini and wordfence-waf.php files (located in your website’s htdocs folder), and if you move from one environment to another, it can result in a 500 error (critical error). Either adjust the hardcoded path or simply remove the Wordfence content from the file.

## Completely Optional Extra

Wordfence themselves have a thorough article that details their guidelines on migrations which you can view here:https://www.wordfence.com/help/advanced/remove-or-reset/#migrate-with-wordfence

If you don’t need everything, Wordfence has saved previously, a clean-up may not be a bad idea, and it gives you a chance to review your security settings upon reactivation. This shouldn’t be necessary for migration purposes, but if you wish to do this, you can head to:

Dashboard > Wordfence > Dashboard > General Wordfence Options

From here, select the last option in the tab as shown below:

You can also export your settings by clicking the IMPORT/EXPORT OPTIONS button if you wish to do so.

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

