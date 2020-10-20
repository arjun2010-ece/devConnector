# devConnector

Technollogies used is:

NodeJS expressJS, React, Redux.
```

-> User model will have only that much fields that you need for signup.
-> Profile model willl have all the other fields for storing data.

```
And a one-to-one relationship exists between User and Profile Model.

In Profile section, Experience and Education will be an ARRAY field(or array of objects.).
Why?
The reason is simple because a single person will have more than one experience and same for education like bachelors and Masters.
Thats why.

On top of that there will be a separate endpoint for /experience and /education.
And make a experience/education object and assign with JS unshift().
```
ex::  
const profile = await Profile.findOne({user: req.user._id);

profile.experience.unshift(newExpObject); //experience array added newExpObject.
await profile.save();
```
===============================
-> When you delete the profile then you need to delete the user also.


==============================

deleteing an experience in profile::
==================================
first find index of experience id and then splice it with that index.
For finding indexOf, we need an simple array that isof IDs.

e.g::
```
 const profile = await Profile.findOne({ user: req.user.id });
     // Get remove index
    const removeIndex = profile.experience.map(item => item.id).indexOf(req.params.exp_id);
    profile.experience.splice(removeIndex, 1);
    await profile.save();
```


