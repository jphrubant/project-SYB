#  Project SYB

## Description
SYB is a peer-to-peer sharing platform for un-motorized, free-to-use, water-sports vehicles.

## User Stories
- View and request to book e.g. a paddleboard, canoe, kayak, inflatable or rowing boat 
from other private persons for one day
- Add own boats, edit or delete them, define availability
- Receive and manage incoming request
- Signup / login /logout

## Backlog
- Geo-position and map
- User profiles
- Rating of bookings
- App sends e-mails
- Communicate via the platform 
- Bookings conditions
- Extended Search by name or features
- Favorites
- Enable date-range search
- Enable multi-day bookings
- Include commercial aspects

## Handlebars Views
- Navigation
- addboat.hbs
- bookings.hbs
- edit-boat.hbs
- index.hbs
- layout.hbs
- log-in.hbs
- myboats.hbs
- sign-up.hbs

## Models

User model
```
{
    firstName: {
        type: String,
    },
    lastName: {
        type: String,
    },
    email: {
        type: String,
        required: true,
        unique: true
    },
    password: {
        type: String,
        required: true,
        unique: true
    },
    phoneNumber: {
        type: String
    },
    listings: [{
        type: Schema.Types.ObjectId,
        ref: "Listing"
    }],
    bookings: [{
        type: Schema.Types.ObjectId,
        ref: "Booking"
    }],
    favourites: [{
        type: Schema.Types.ObjectId,
        ref: "Listing"
    }],
}, {
    timestamps: {
        createdAt: "created_at",
        updatedAt: "updated_at"
    }
}
```
Listing model
```
{
    name: {
      type: String,
      required: true,
      unique: true
    },
    type: {
      type: String,
      required: true,
      enum: ["canoe", "kayak", "rowing", "inflatable", "paddle", "boat"]
    },
    locationAddress: {
      street: { type: String, required: true },
      streetNumber: { type: String, required: true },
      city: { type: String, required: true },
      province: { type: String },
      country: {type: String }
    },
    locationGeoCoord: {
      type: { type: String },
      coordinates: [] 
    },
    notAvailableDates: {
      type: [Date]
    },
    imageURL: {
      type: String,
      default: "https://image.flaticon.com/icons/svg/0/300.svg",
      required: true
    },
    description: {
      type: String,
      required: true

    },
    forMaxNumOfUsers: {
      type: Number,
      required: true
    },
    brand: {
      type: String,
    }
},
  {
    timestamps: {
      createdAt: "created_at",
      updatedAt: "updated_at"
  }
}
```
Booking Model
```
{
    ownerId: {
        type: Schema.Types.ObjectId,
        ref: 'User',
        required: true
    },
    borrowerId: {
        type: Schema.Types.ObjectId,
        ref: 'User',
        required: true
    },
    listingId: {
        type: Schema.Types.ObjectId,
        ref: 'Listing',
        required: true
    },
    bookingStart: {
        type: Date,
        default: Date.now,
        required: true
    },
    bookingEnd: {
        type: Date
    },
    status: {
        type: String,
        enum: ['pending', 'accepted', 'declined'],
        required:true
    }
},
    {
        timestamps: {
            createdAt: "created_at",
            updatedAt: "updated_at"
        }
    }
```

## Backend Endpoints

auth.js
```
authRouter.post("/")
authRouter.get("/")
```
login.js
```
loginRouter.get("/")
loginRouter.post("/")
```
bookings.js
```
router.post("/:id")
router.post("/request/:id")
router.get("/")
```
index.js
```
router.get("/logout")
router.get('/')
```
myboats.js
```
router.get("/edit/:id")
router.post('/edit/:listingId')
router.post("/delete/:id")
outer.post("/add")
router.get("/addboat")
router.get("/")
```

## Links
- [Trello](https://trello.com/b/vI6yENH0/ironhack-project-syb)
- [Git](https://github.com/jphrubant/project-SYB)
- [Slides](https://docs.google.com/presentation/d/1L6BvUfvTx_Pbqtca1E9k2xEBB91hLHqw7YMOgznhVn0/edit)
