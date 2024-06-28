# Project 01

## Frontend Notes

### Pages:

1. `Homepage`: contain basic homepage layout with:

   - **header image**,
   - **live contests list**,
   - **upcoming contests list**
   - and **faqs section at the bottom**.

2. `Contest Page`: contain contest specific information (filtered by item `id` value.)
3. `Order Page`: contain user order summaries (**data fetched from the backend and can be altered accordingly**).
4. `Cart Page`: contains all user added items list in cart.
5. `About Page`: contain information about website
6. `Contact Page`: contact details for sure.

### functionalities and features

1. `Add to cart logic`: add to cart option will update the cart value by 1 when user is logged-in,
   can be trigger with `updateCart` function which will increment cart value by along with the
   item information which we'll fetch from the backend.
2. `Filtering logic`: provide a component on the frontend side, which will be having option to
   filter out thing based **price range**, **category**, **date**, and **status**.
3. `pagination logic`: providing the only max 10 items to be loaded first, and then we will provide
   pages option for next 6 pages, so we'll have tracked record for pages no to give next 6 after
   that number.
