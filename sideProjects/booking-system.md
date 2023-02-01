# Problems faced when building a booking system

1.  ### Determine if item has already been added to cart

    Item uniqueness is determined by the 'time slot' it is assigned to, the booking duration and the unit (units to book, e.g. seats for cinema).

    - User are not able to book a unit that has already been booked.

      e.g. user have added seat A to his cart, he will not be able to add it to cart again

    - User are not able to book a unit with a time slot that user have booked previously

      e.g. if **8AM - 10AM** slot is booked, user should not be able to book **9AM - 10AM** slot with the same unit

    The first scenario is easily achievable by just checking the unitId whenever the item is fetched, the second scenario however is a bit tricky to handle.

    2 ways of achieving this :

    1. Check on client side

       Filter out results that user have already added to their cart.

       e.g. if **8AM - 10AM** slot is already added to cart by user, whenever book venue page fetch for available event units, it will filter out unavailable timeslots in client side

    2. Check on server side

       Call api whenever user adds something to cart, it will track down the time slot the user is adding to his cart.

       when client fetches from server again, it will filter out results based on previously added item.

       **Challenges** : hard to work for a non logged in user
