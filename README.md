# CS 360: Mobile Architect & Programming Portfolio

## Inventory Tracking Android App

This repository contains my completed Project Three artifact for CS 360: Mobile Architect and Programming. The project is a fully functional Android inventory tracking app, built from an initial UI design through a complete working app with a login system, a persistent SQLite database, full CRUD functionality, and SMS permission handling.

## Project Reflection

### App requirements and goals

This app was designed to help warehouse employees, supervisors, and small business owners keep accurate track of stock levels. The core user need was a fast, simple way to see what is currently in stock, add new items as they come in, remove items that are gone, and adjust quantities as products move in and out during a shift. A secondary need was making sure nobody has to constantly babysit the stock screen, which is why the app also sends a text alert the moment an item quantity drops to zero.

### Screens, features, and user-centered design

The app is built around three main screens: a login and account creation screen, a main inventory grid, and an add/edit item screen. Each screen was designed around a single clear task rather than cramming multiple actions into one place. The login screen only asks for a username and password and offers an obvious path for brand new users to create an account. The inventory grid keeps the most important information, item name and quantity, front and center, with simple Edit and Delete buttons on every row so a user never has to dig through menus to make a change. The add/edit screen reuses the same simple layout for both adding and editing, which keeps the app consistent and easier to learn. These choices were successful because they kept the number of steps needed for any common task as low as possible, which matters for users who are moving quickly during a busy shift.

### Coding approach and strategies

I approached the coding process by building and testing one layer at a time instead of trying to write the entire app at once. I started with the login system and database shell, confirmed it worked completely on its own, then moved to the inventory grid and full CRUD operations, and only added the SMS permission logic once the database and screens were already stable. I also kept the app's layers separate on purpose, with the database logic living entirely in one class, the UI logic in the activities, and the SMS logic isolated to the one screen where it actually mattered. This made debugging far easier, since when something broke, I usually already knew which layer to look in first. I plan to keep using this same incremental, one-piece-at-a-time approach in future projects, since it made problems much easier to isolate and fix.

### Testing process

I tested constantly throughout development using the Android Emulator rather than waiting until the end. Every new feature, from the login check to each CRUD action to the SMS permission flow, was tested immediately after being written, including specifically testing both the permission-granted and permission-denied paths for the SMS feature. This process mattered because it caught real problems early, including a stale build issue where old code kept running even after I had written new code, which I only caught by paying close attention to what the Build tab was actually reporting. Testing early also confirmed that the database was truly persistent, since closing and reopening the app still showed the same saved inventory items.

### Where I had to innovate

The most challenging part of the project was figuring out how to handle the SMS permission request in a way that would not break the rest of the app if a user said no. Instead of building a separate screen dedicated to permissions, I chose to request permission automatically the first time the inventory screen loads, and then check that same permission status again independently whenever an item's quantity reaches zero. This meant the feature could work seamlessly if allowed, and fail silently without any crash or broken functionality if denied, which matched the real-world expectation that optional features should never take down the rest of an app.

### Where I was most successful

I am most proud of the database and CRUD implementation. Building a single reusable SQLiteOpenHelper class that manages both the user accounts table and the inventory table, while keeping every create, read, update, and delete operation cleanly separated into its own method, made the rest of the app much easier to build on top of. That structure is something I would confidently reuse as a starting point for future Android projects.
