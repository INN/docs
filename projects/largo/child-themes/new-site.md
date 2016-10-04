# Setup Process for Each Member Site

You've probably [just installed the largo-umbrella](/onboarding/largo-umbrella-setup.md) or updated your database! Huzzah!

However, you'll need to do a brief setup for **each** member site you work with.

You've downloaded a production database, so we need to update some settings in WordPress to tell it it's running on your virtual machine.

We'll use the shorthand `project.org` to represent a sub-site of the Largo umbrella, and you should substitute in the site you want to get access to. For your purposes, this might instead be `investigatemidwest.org` or `iowawatch.org`.

### 1. Log in to the main dashboard of your multisite and navigate to Network > Sites

The Largo Network of Sites:
[http://vagrant.dev/wp-admin/network/sites.php](http://vagrant.dev/wp-admin/network/sites.php)

## 2. In the list of Network Sites, find your `project.org` site and click Edit.

## 3. Find the blog ID of `project.org`.

We're going to need the numeric WP Blog ID associated with `project.org` for further steps.

Find the ID number in the browser's current URL. For example, if the URL is `http://vagrant.dev/wp-admin/network/site-info.php?id=53` then the ID is 53. Copy this down.

You will want to leave this tab open we will be returning shortly.

## 4. Convert `project.org` to `project.vagrant.dev`.

This process is similar to what we did in replacing `largoproject.wpengine.com` with `vagrant.dev` for the main WordPress network site, only we'll be selecting a different set of tables to search through based on the blog ID you now have copied down above.

1. Open [http://vagrant.dev/searchreplacedb2.php](http://vagrant.dev/searchreplacedb2.php), make sure the box is checked for "Pre-populate the DB values", and click the "Submit" button.

2. You will see a multi-select of database tables. Ctrl-click or shift-click to choose the tables prefixed with `wp_#_`, where # is the ID you copied down. *i.e. If the ID was 53, then you'd need tables with the prefix `wp_53_`.*

3. Check the box for "Leave GUID column unchanged?", and then click the "Continue" button. You may get a pop-up warning you to make sure you selected the right tables, click "OK" to continue.

3. You should now be at the screen for actually replacing the text, titled **What to replace?**.

Search for your particular `project.org` main site address and replace with `project.vagrant.dev`.
Example: If you're working with `investigatemidwest.org` then you should replace that with `investigatemidwest.vagrant.dev`.

4. Click the "Submit Search string" button, and click "OK" in the pop-up to confirm that you want to do it.

If the change is successful, you should see a final summary screen with details similar to the following:

    ```
    In the process of replacing "investigatemidwest.org" with "investigatemidwest.vagrant.dev" we scanned 9 tables with a total of 18694 rows, 581 cells were changed and 579 db update performed and it all took 6.668104 seconds.
    ```

## 5. Change `project.org` to `project.vagrant.dev` in WordPress Admin.

We also need to change the settings in the Largo-umbrella network site so that `project.org` is changed to `project.vagrant.dev`. This will be the final step before we can visit `http://project.vagrant.dev` in the browser.

1. Return to the tab for the site you just preformed the search-and-replance on. Refresh for good measure.

2. In the **Site Address (URL)** text field, change `project.org` to `project.vagrant.dev` substituting in the sub-site's actual name.

3. Click on the "Settings" tab.

4. Change the **Siteurl** text field from `http://project.org` to `http://project.vagrant.dev`.

5. Scroll all the way to the bottom and click the "Save Changes" button.

6. **SNAPSHOT**: Let's save our progress now. In your command line, take another snapshot with (substitute in the name of the project):

```
$ vagrant snapshot take default after_project_rename_domain
```

## 6. Grant superadmin access to the member site

1. Staying within the same site, find the **Users** tab at the top and click it.

2. Under "Add Existing User", enter `superadmin` as the username and select the "Administrator" role.

**SNAPSHOT**: Let's save our progress now. In your command line, take another snapshot with (substitute in the name of the project):

```
$ vagrant snapshot take default after_project_adding_superadmin
```

## 7. Finally, edit your host computer's `/etc/hosts` file to allow the new project.vagrant.dev to be used

NOTE: The hosts file entry must only be set *once*. It's not necessary when reloading the database.

```
$ sudo nano /etc/hosts
```
Enter your password, use the arrow keys to position the cursor at the end of the file and add the following line, substituting `project` for your `project.org` name:
```
192.168.33.10 project.vagrant.dev
```

Then use Ctrl-O to save your changes and Ctrl-X to exit the editor. This tells your computer where to resolve the subdomain.

## Done!
