# mettle_tsp

I wrote this to solve the traveling salesman problem three ways and draw every step. It's [Mettle](https://github.com/The-Mettle-Project/Mettle), and the window is [MythicUI](https://github.com/Lex-Dellimere/MythicUI), my GUI library.

![2-opt at work](docs/two-opt.webp)

Nearest neighbour builds the first tour by always going to the closest city it hasn't visited yet. Then 2-opt tests every pair of edges and flips the stretch between them whenever that makes the tour shorter. It stops once no flip helps.

Simulated annealing starts from a random order and flips random stretches. It always keeps a shorter tour and sometimes keeps a longer one, with a chance of exp(-increase / temperature), and the temperature drops every step.

Exhaustive search tries every order that starts at city 0, so its answer is the shortest tour there is. It's capped at 10 cities, which already have 362,880 orders.

Click the map to add a city and right click a city to remove it.

## Build and run

You'll need the Mettle compiler and mbuild. mbuild fetches MythicUI from the registry.

```bash
mbuild run tsp
```

```bash
mbuild run check
```

The check makes sure every result is a tour, that 2-opt never makes the nearest neighbour tour longer, and that exhaustive search matches a separate brute force on 30 maps of 4 to 9 cities.

## Files

- `src/tsp.mettle` has the three solvers, which run one step per call.
- `src/app.mettle` draws the window and `src/main.mettle` opens it.
- `tests/check.mettle` is the check.
- `tools/snapshot.mettle` renders the app without a screen at a few points in a run and saves PNGs to `build/shots/`.
- `tools/compare.mettle` measures how far each method's tours are from the shortest.
- `tools/frames.mettle` saves a PNG for every frame of a run, for the animation.

`snapshot` and `frames` take an optional scale as their first argument, so `mbuild run frames -- 2` renders at twice the size.

## License

Apache-2.0
