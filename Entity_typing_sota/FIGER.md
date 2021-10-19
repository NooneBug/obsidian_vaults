Dataset defined by [[2012 Ling - Fine-Grained Entity Recognition]].

It contains 112 types extracted from FreeBase : 

*While Freebase tags are comprehensive, they are also noisy (often created by non-expert users). As a result, we need to filter irrelevant types to reduce the data noise. We only keep well-maintained types (the ones with curated names, e.g. /location/city) with more than 5 ground instances in Freebase. We further refine the types by manually merging too specific types, e.g. /olympics/olympic games and /soccer/football world cup are merged into Sports Event. In the end, 112 types remain for use as our tag set, denoted as T*

FIGER is a [[Datasets with hierarchical sets of types]]

This is the first dataset built using [[Distant Supervision]], for each entity, authors found its wikipedia page and use it to retrieve its types in freebase.

Training is extracted from Wikipedia, test comes from 18 up-to-date news reports manually annotated using the tag set T 