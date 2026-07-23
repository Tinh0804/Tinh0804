# Mobile rendering fix

The previous README used two side-by-side GitHub Stats images and a contribution snake image. On mobile, failed external requests rendered their alt text instead of cards. Two-column HTML tables were also compressed.

This revision:

- removes the two unreliable stats cards;
- keeps the responsive activity graph;
- temporarily removes the snake from README until the `output` branch exists;
- converts two-column tables into stacked sections for small screens;
- retains all local artwork at `width="100%"`.

## Re-enable the contribution snake

1. Push `.github/workflows/snake.yml` to the profile repository.
2. Open **Actions → Generate contribution snake → Run workflow**.
3. Confirm that the `output` branch contains both SVG files.
4. Add the `<picture>` block back to README only after those URLs open successfully.
