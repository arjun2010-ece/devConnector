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
Note:: Its also an example of deleting from an nested Array of Objects array.

==========================================================
Post model has one to Many relationships with the User Model because One user can create many Posts and a single post will always belongs to only one User.
At the same time a post can be liked by many user so the schema will be like this::
The field "likes will be an array of objects where each user will be pointed to liked users.Since many users can like a single posts.


Here check the comments attribute also as its an array of Objects while each comment object has user, text, name,avatar.


```
const PostSchema = new Schema({
  user: {
    type: Schema.Types.ObjectId,
    ref: 'users'
  },
  text: {
    type: String,
    required: true
  },
  name: {
    type: String
  },
  likes: [
    {
      user: {
        type: Schema.Types.ObjectId,
        ref: 'users'
      }
    }
  ],
  comments: [
    {
      user: {
        type: Schema.Types.ObjectId,
        ref: 'users'
      },
      text: {
        type: String,
        required: true
      },
      name: {
        type: String
      },
      avatar: {
        type: String
      },
      date: {
        type: Date,
        default: Date.now
      }
    }
  ],
  date: {
    type: Date,
    default: Date.now
  }
});
```







