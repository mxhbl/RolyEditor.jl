# RolyEditor.jl

A terminal editor for [Roly.jl](https://github.com/goodrichgroup/Roly.jl) binding rules, built on
[Tachikoma.jl](https://github.com/kahliburke/Tachikoma.jl).

`editrules` builds a set of binding rules geometrically and returns it; `editpolyform` builds a
polyform and returns it as a `Roly.Polyform`.

## Installation

Roly is not registered, so it is installed from its repository. RolyEditor names that repository
as the source of its own dependency, so adding RolyEditor is enough:

```julia
using Pkg
Pkg.add(url="https://github.com/goodrichgroup/RolyEditor.jl")
```

## Usage

```julia
using Roly
using RolyEditor

rules = editrules(UnitSquare)                      # any species, in 2D or 3D
rules = editrules([UnitSquare, UnitTriangle])      # several shapes to choose from
rules = editrules(rules)                           # carry on from an existing system
bonds = editrules(UnitSquare; output=:bonds)       # an n×4 integer matrix instead

poly = editpolyform(UnitCube)                      # the polyform, not the rules
poly = editpolyform(UnitCube; addressable=true)    # a species per particle
poly = editpolyform(poly)                          # carry on from a polyform
```

`q` accepts and returns, and the editor's own key legend is the left-hand pane.

## What it does

Binding rules can be arrived at two ways, and both are on screen together.

**Placing particles.** Each attachment seats a copy of a species against one of the polyform's
free binding sites. The rules are then read off every *pair* of placed particles rather than only
the pairs that were attached, so closing a ring reports bonds no attachment named: three
attachments building a 2×2 block reveal a fourth pair, where the last square meets a second
neighbour.

**Editing the table.** A cursor over the interaction matrix bonds a pair of colors directly, and a
hand edit holds against whatever the geometry goes on to produce. Where the matrix is too large to
show, the list of bonding pairs takes the pane and the pair the cursor names is written above it.

Polyforms are built in construction windows: `n` opens another and `w` cycles between them. The
rules come off all of them at once, so an arrangement stays on the books while the next is built
beside it. `f` turns on fully addressable mode, which gives every placement a species o

## Documentationf its own,
so each bond names one particular pair of particles rather than a pair of species.

A fourth pane enumerates the polyforms the rules allow, which can be triggered by pressing `e`.

3D species are drawn in isometric projection as braille wireframes.
`[` and `]` step the camera through eight viewpoints, shared by every pane.

The full key reference is the docstring of `editrules`, and the editor's own sidebar lists the
keys of whichever pane has the focus.
