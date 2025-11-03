# Overview

## Packs

Looking in the [FoundryVTT PF2e Github Repo](https://github.com/foundryvtt/pf2e)
you will see that classes that are built into the system are all registered
under, `/packs/classes`, located [here](https://github.com/foundryvtt/pf2e/tree/v13-dev/packs/classes).
In addition to the class json, here are a list of different "class data definitions":

- `packs/classfeatures`
- `packs/feats/{class-name}`

## Data Defintition

Found at `pf2e/src/module/item/class/data.ts`, you'll find how the data from these
"packs" are defined and are related to be referenced within the application. I'm
assuming that once you have defined the "pack" for your class, you'll need someway
to "unpack" our pack from a module into the core pf2e system, which means you'll need
to "re-unpack" after a pf2e update which would overwrite this. There is also, located
at [`pf2e/src/module/item/class/values.ts`](https://github.com/foundryvtt/pf2e/src/module/item/class/values.ts)
a list of all of the classes the system should expect, we would need to inject our class
into this `CLASS_TRAITS` set.

```typescript
// module/item/class/values.ts
/**
 * Classes don't have traits other than rarities, but both feats, spells, and other items can have traits corresponding
 * with a class
 */
export const CLASS_TRAITS = new Set([
  "alchemist",
  "animist",
  "barbarian",
  "bard",
  "champion",
  "cleric",
  "commander",
  "druid",
  "exemplar",
  "fighter",
  "guardian",
  "gunslinger",
  "kineticist",
  "inventor",
  "investigator",
  "magus",
  "monk",
  "oracle",
  "psychic",
  "ranger",
  "rogue",
  "sorcerer",
  "summoner",
  "swashbuckler",
  "thaumaturge",
  "witch",
  "wizard",
] as const);
```

## References

[pf2e witcher class](https://github.com/EregionArts/pf2e-witcher)

I'm noticing that the "packs" for all of these are compiled to some binary type. I'm assuming these should still
be originally created as a JSON with some sort of workflow to decompile them possible, trying to figure that out
from these reference sources

A lot of the definitions for the class packs appear to be within the `module.json`

It does look like we need to get these json compiled into .ldb format (level-db) which can be a part of
a packing and unpacking process handled by foundry once the "packs" are registered, by module.json.
Review the "scripts" that exists int he above witcher class to understand how "injections" can occur.

Found the official [Creating a PF2e Content Module](https://github.com/foundryvtt/pf2e/wiki/Creating-a-PF2e-Content-Module)

The [PF2e Animist actually has Json packs!](https://github.com/reyzor1991/pf2e-animist)
