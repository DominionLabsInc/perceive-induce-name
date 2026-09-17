# Perceive, Induce, Name

**Vision in a cognitive substrate with no perceptual model: algorithms recover structure, the substrate
learns to name it, and it abstains when it has not.**

Stefan Ragland, Dominion Labs Research & Development. Published 8 September 2026.

- Paper (PDF): [`paper/perceive-induce-name.pdf`](paper/perceive-induce-name.pdf)
- Paper (web): <https://dmnlabs.org/research/perceive-induce-name/>
- Contact: research@dmnlabs.org

This repository carries the paper and the measurements behind every number in it. The studies were run
against a live cognitive substrate; the substrate itself is not distributed here. What is here is the
record: for each study, the manifest the run wrote and the images it was shown.

## What the paper reports

Seeing is treated as two capabilities rather than one. Recovering the structure of an image, meaning where
the coherent objects are and their shape, size, position and colour, is done by classical algorithms that
learn nothing. Attaching a name to a category is a learning problem, and the substrate does it by
induction over the features perception reports, naming a new instance by a rule it induced from a few
labelled examples and declining when it has learned no rule that fits.

| Study | Scale | Result | Data |
|---|---|---|---|
| Headline evaluation | 3 categories, 31 images | perception 100% shape and 100% colour; naming recall 100%, abstention 100%, false namings 0, model calls 0. With the learned rules removed, recall 0% and abstention 100% | [`data/perceive-eval.json`](data/perceive-eval.json) |
| The same loop at scale | 8 categories, 149 images | mean naming recall 95.8%, abstention 100%, false namings 0, model calls 0 | [`data/perceive-eval2.json`](data/perceive-eval2.json) |
| What a name costs to teach | 1 to 4 labelled examples; 0 to 2 counter-examples | one example is refused as a case rather than a generalisation; three give full recall; the second counter-example is what restores full abstention | [`data/perceive-eval2.json`](data/perceive-eval2.json) |
| Operating range of perception | noise, blur, rotation, desaturation, occlusion, apparent size | colour is the most robust measurement and shape the first to go; the minimum reported object area is a stated parameter | [`data/perceive-eval2.json`](data/perceive-eval2.json) |
| Naming when the examples do not decide | 32 inductions, 416 images | naming on any surviving hypothesis produces 26 false namings out of 192 non-members; naming only what every hypothesis accepts produces 0, at 72.9% recall | [`data/perceive-ambig-01.json`](data/perceive-ambig-01.json) |
| Closing the ambiguity | 16 undetermined inductions | supplying the case the substrate asks for closes all 16, in a mean of 2.6 rounds; randomly chosen examples close 1 of 16 | [`data/perceive-ambig-02.json`](data/perceive-ambig-02.json) |

Across every study, naming was performed by the substrate's own reasoning over rules it had induced, and
no language model was called at any point.

## Layout

```
paper/     the paper as PDF, and as a self-contained web page with its stylesheet
data/      one manifest per study, written by the run itself
stimuli/   the images each study drew and was shown, one directory per study
```

Each manifest is the file the experiment wrote at the end of its run, unedited. Every figure and table in
the paper is computed from these files, and [`data/README.md`](data/README.md) says which field carries
which claim.

## How the studies were run

Each study draws its own stimuli, teaches the substrate what perception reported about them, asks it to
induce a category from a few labelled examples, and then asks it to name held-out instances it was never
taught. Scoring happens afterwards. The expected answer is never supplied to the reasoner, only the
question.

Two conventions are worth stating because they matter for reading the data. A size band such as `small`
is a property of perceived area rather than of the radius an object was drawn at, so a circle, a square
and a triangle at one radius do not share it; the later studies therefore select a stimulus by perceiving
it first and using it only if perception reports the features the condition requires. And an induction
that finds more than one hypothesis consistent with its examples keeps them all, so the manifests record
a list of hypotheses, not a single rule.

## Citation

```bibtex
@techreport{ragland2026perceive,
  title       = {Perceive, Induce, Name: vision in a cognitive substrate with no perceptual model},
  author      = {Ragland, Stefan},
  institution = {Dominion Labs},
  year        = {2026},
  month       = {9},
  url         = {https://dmnlabs.org/research/perceive-induce-name/}
}
```

## License

The paper, the data and the stimuli are released under
[Creative Commons Attribution 4.0](LICENSE). Please cite the paper if you use them.
