Summary of changes

I found and fixed five main issues:

1. Fixed the SQL search condition by adding parentheses around the OR conditions so the status filter works correctly.
2. Removed the unnecessary Thread.sleep() delay from the backend.
3. Fixed the frontend request race condition using AbortController, so old search requests do not overwrite newer results.
4. Reset the page to page 1 when the search or status filter changes.
5. Added validation for API inputs. Invalid status, page, and page size now return a 400 response. The maximum page size is 100.

What I did not change

I did not rewrite the existing application or make unrelated changes. I kept the patch small and focused on the problems I found during testing.

Biggest remaining risk

The application may have performance problems when the number of tasks becomes very large. More investigation would be needed to make database searching and pagination more efficient.

Tools and AI used

I used ChatGPT and Claude to help me understand the code, find possible bugs, and understand different ways to fix them. I tested the suggested fixes myself and made the code changes after understanding what each change does.
