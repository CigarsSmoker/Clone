By default, out of the box, uMatrix blocks all 3rd-party script, but allows 1st-party scripts to run on any web site.

If you wish, you can set up uMatrix to block all scripts by default everywhere with only a few clicks.

By default, 1st-party scripts are not blocked:

![a](https://user-images.githubusercontent.com/585534/33189052-21868182-d06d-11e7-9447-69a2f12334c4.png)

Select the global scope:

![a](https://user-images.githubusercontent.com/585534/33189061-3a4bea9a-d06d-11e7-99ba-ab95c50f5484.png)

Create a block rule for all scripts (`* * script block`):

![a](https://user-images.githubusercontent.com/585534/33189068-52538652-d06d-11e7-9f3a-3329d0bd74ab.png)

If you want the approach of block 1st-party script for good, you will want to persist the new block rule:

![a](https://user-images.githubusercontent.com/585534/33189093-9d7f32ac-d06d-11e7-9b54-728b7cb048f1.png)

At this poin, all 1st-party scripts are blocked everywhere. On the site where you created the rule:

![a](https://user-images.githubusercontent.com/585534/33189108-bf860420-d06d-11e7-8617-08f7b9e2b96f.png)

And all other sites:

![a](https://user-images.githubusercontent.com/585534/33189144-123ff018-d06e-11e7-82f2-62920f864660.png)
