# bad args

    Code
      recipe(Species ~ ., data = three_class) %>% step_embed(Sepal.Length, outcome = vars(
        Species)) %>% prep(training = three_class, retain = TRUE)
    Condition
      Error in `step_embed()`:
      Caused by error in `prep()`:
      ! All columns selected for the step should be string, factor, or ordered.

# check_name() is used

    Code
      prep(rec, training = dat)
    Condition
      Error in `cnd_type()`:
      ! `cnd` is not a condition object.

# empty printing

    Code
      rec
    Message
      
      -- Recipe ----------------------------------------------------------------------
      
      -- Inputs 
      Number of variables by role
      outcome:    1
      predictor: 10
      
      -- Operations 
      * Embedding of factors via tensorflow for: <none>

---

    Code
      rec
    Message
      
      -- Recipe ----------------------------------------------------------------------
      
      -- Inputs 
      Number of variables by role
      outcome:    1
      predictor: 10
      
      -- Training information 
      Training data contained 32 data points and no incomplete rows.
      
      -- Operations 
      * Embedding of factors via tensorflow for: <none> | Trained

# printing

    Code
      print(rec)
    Message
      
      -- Recipe ----------------------------------------------------------------------
      
      -- Inputs 
      Number of variables by role
      outcome:   1
      predictor: 3
      
      -- Operations 
      * Embedding of factors via tensorflow for: x3

