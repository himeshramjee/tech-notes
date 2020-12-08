GraphQL - Notes from Roberts talk

1. Efficiency
   1. Overfetching - responses contained too much data
   1. Underfetching - too little data, so more network requests
1. Type safety
1. Domain modelling
   1. Domain-driven design
   1. Shared language for different stakeholders making modelling and design functions more intuitive
   1. Problems can be described in natural language
1. AuthN and AuthZ
   1. Neither live within GraphQL (not a problem for this domain)
   1. AuthN lives at top prototol layer
   1. AuthZ lives at mid business layer
1. Promotes up front design which
1. Do not place auth and business logic in GraphQL layer
1. Ensure you educate your team and business stakeholders
1. Build the simplest queries first and gradually expand
1. Check out
   1. AWS AppSync
   1. ApolloGraphQl
