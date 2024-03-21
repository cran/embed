# factor encoded predictor

    Code
      new_values_ch <- bake(class_test, new_data = new_dat_ch, contains("embed"))
    Condition
      Warning:
      ! There was 1 column that was a factor when the recipe was prepped:
      * `x3`
      i This may cause errors when processing new data.

---

    Code
      new_values_ch <- bake(class_test, new_data = new_dat_ch, contains("embed"))
    Condition
      Warning:
      ! There was 1 column that was a factor when the recipe was prepped:
      * `x3`
      i This may cause errors when processing new data.

# bad args

    Code
      recipe(Species ~ ., data = three_class) %>% step_embed(Sepal.Length, outcome = vars(
        Species)) %>% prep(training = three_class, retain = TRUE)
    Condition
      Error in `step_embed()`:
      Caused by error in `prep()`:
      x All columns selected for the step should be string, factor, or ordered.
      * 1 double variable found: `Sepal.Length`

# check_name() is used

    Code
      prep(rec, training = dat)
    Condition
      Error in `step_embed()`:
      Caused by error in `bake()`:
      ! Name collision occurred. The following variable names already exist:
      * `x3_embed_1`

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

# keep_original_cols - can prep recipes with it missing

    Code
      rec <- prep(rec)
    Condition
      Warning:
      `keep_original_cols` was added to `step_embed()` after this recipe was created.
      i Regenerate your recipe to avoid this warning.

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

---

    Code
      prep(rec)
    Message
      
      -- Recipe ----------------------------------------------------------------------
      
      -- Inputs 
      Number of variables by role
      outcome:   1
      predictor: 3
      
      -- Training information 
      Training data contained 500 data points and no incomplete rows.
      
      -- Operations 
      * Embedding of factors via tensorflow for: x3 | Trained

