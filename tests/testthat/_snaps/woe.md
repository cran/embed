# woe_table do not accept different length inputs

    Code
      embed:::woe_table(rep(c(0, 1), 20), rep(letters[1:4], 5))
    Condition
      Error in `embed:::woe_table()`:
      ! 'outcome' must have exactly 2 categories (has 4)

# woe_table accepts only outcome with 2 distinct categories

    Code
      embed:::woe_table(rep(letters[1:3], 10), rep(c(0, 1, 2), 10))
    Condition
      Error in `embed:::woe_table()`:
      ! 'outcome' must have exactly 2 categories (has 3)

---

    Code
      embed:::woe_table(rep(letters[1:3], 10), rep(c(0), 30))
    Condition
      Error in `embed:::woe_table()`:
      ! 'outcome' must have exactly 2 categories (has 1)

---

    Code
      embed:::woe_table(df$x2, df$x1)
    Condition
      Error in `embed:::woe_table()`:
      ! 'outcome' must have exactly 2 categories (has 3)

# add_woe accepts only outcome with 2 distinct categories

    Code
      dictionary(df %>% filter(y %in% "B"), "y")
    Condition
      Error in `dictionary()`:
      ! 'outcome' must have exactly 2 categories (has 1)

# add_woe do not accept dictionary with unexpected layout

    Code
      add_woe(df, outcome = "y", x1, dictionary = iris)
    Condition
      Error in `add_woe()`:
      ! column "variable" is missing in dictionary.

---

    Code
      add_woe(df, outcome = "y", x1, dictionary = iris %>% mutate(variable = 1))
    Condition
      Error in `add_woe()`:
      ! column "predictor" is missing in dictionary.

# step_woe

    Code
      woe_models <- prep(rec, training = credit_tr)
    Condition
      Warning:
      Some columns used by `step_woe()` have categories with less than 10 values: 'Home', 'Job'

---

    Code
      prep(rec_all_nominal, training = credit_tr, verbose = TRUE)
    Output
      oper 1 step woe [training] 
    Condition
      Warning:
      Some columns used by `step_woe()` have categories with less than 10 values: 'Home', 'Job'
    Output
      The retained training set is ~ 0.14 Mb  in memory.
      
    Message
      
      -- Recipe ----------------------------------------------------------------------
      
      -- Inputs 
      Number of variables by role
      outcome:    1
      predictor: 13
      
      -- Training information 
      Training data contained 2000 data points and 186 incomplete rows.
      
      -- Operations 
      * WoE version against outcome Status for: Home, Marital, Records, Job | Trained

---

    Code
      prep(rec_all_numeric, training = credit_tr)
    Condition
      Error in `step_woe()`:
      Caused by error in `prep()`:
      ! All columns selected for the step should be string, factor, or ordered.

# 2-level factors

    Code
      recipe(Species ~ ., data = iris3) %>% step_woe(group, outcome = vars(Species)) %>%
        prep()
    Condition
      Error in `step_woe()`:
      Caused by error in `dictionary()`:
      ! 'outcome' must have exactly 2 categories (has 3)

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
      * WoE version against outcome mpg for: <none>

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
    Condition
      Warning:
      Unknown or uninitialised column: `variable`.
    Message
      * WoE version against outcome mpg for: <none> | Trained

# keep_original_cols - can prep recipes with it missing

    Code
      rec <- prep(rec)
    Condition
      Warning:
      'keep_original_cols' was added to `step_woe()` after this recipe was created.
      Regenerate your recipe to avoid this warning.

# printing

    Code
      print(rec)
    Message
      
      -- Recipe ----------------------------------------------------------------------
      
      -- Inputs 
      Number of variables by role
      outcome:    1
      predictor: 13
      
      -- Operations 
      * WoE version against outcome Status for: Job, Home

---

    Code
      prep(rec)
    Condition
      Warning:
      Some columns used by `step_woe()` have categories with less than 10 values: 'Home', 'Job'
    Message
      
      -- Recipe ----------------------------------------------------------------------
      
      -- Inputs 
      Number of variables by role
      outcome:    1
      predictor: 13
      
      -- Training information 
      Training data contained 4454 data points and 415 incomplete rows.
      
      -- Operations 
      * WoE version against outcome Status for: Job, Home | Trained

