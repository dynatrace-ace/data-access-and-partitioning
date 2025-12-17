## Management Zones to Segments

The team has an "Easytrade" Management zone that they are using to navigate across views

SCREENSHOT SHOW HOW THEY WHERE FILTERING THE SERVICES APP

SCREENSHOT SHOW HOW THEY WHERE FILTERING THE HOSTS APP

In order to do the same in 3rd Gen, we need to configure Segments. 

1. Go to the Segments setting, create a new Segment called App

SCREENSHOT

2. Add the following to the variable, in order to search for the primary_tags

DQL CODE

SCREENSHOT

3. Filter "All Data" using the variable

SCREENSHOT

Notice how previously, the admin team needed to create a Management Zone for every app that was onboarded into Dynatrace, now with 3rd Gen we don't have to do this anymore. If a new team is onboarded with a primary_tags.app = hisptershop, this value will populate automatically

4. Validate if the user could potentially navigate through their 3rd Gen screens

SCREENSHOT

5. If the new apps satisfies the requirements of the team, you can remove the classic views to ensure consistency

SCREENSHOT IAM SETTING TO REMOVE APP

SCREENSHOT CLASSIC APP NOT SHOWING IN 3RD GEN

### Close Up

Now our users can navigate across 3rd Gen apps as they did in classic, and removed some of the classic apps to ensure consistency.

If the 3rd Gen app doesn't satisfy yet the requirements of the team as the classic was, please reach out to us for feedback!