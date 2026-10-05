Summary of changes

I found and fixed five main issues:

1. Fixed the SQL search condition by adding parentheses around the OR conditions so the status filter works correctly.
2. Removed the unnecessary Thread.sleep() delay from the backend.
3. Fixed the frontend request race condition using AbortController, so old search requests do not overwrite newer results.
4. Reset the page to page 1 when the search or status filter changes.
5. Added validation for API inputs. Invalid status, page, and page size now return a 400 response. The maximum page size is 100.

What I did not change

I kept the patch focused. I did not change the current in-memory pagination, add search debouncing, or escape % and _ characters used in SQL LIKE searches. These could be improved later, but I did not want to make unrelated changes during the timebox.

Biggest remaining risk

The controller currently loads all matching rows and then slices the list in Java for pagination. This may become slow and use more memory when the number of tasks grows. With more time, I would move pagination to the database using Spring Pageable or database-level LIMIT/OFFSET.

Tools and AI used

I used ChatGPT and Claude to help me understand the code, find possible bugs, and understand different ways to fix them. I tested the suggested fixes myself and made the code changes after understanding what each change does.
