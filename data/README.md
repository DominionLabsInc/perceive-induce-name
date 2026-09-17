# Data

One manifest per study, exactly as the run wrote it. Nothing here is edited after the fact.

## `perceive-eval.json`: the headline evaluation

Three categories over 31 images, scored twice: once with the learned rules present and once with them
removed.

| Field | What it carries |
|---|---|
| `overall.perception_shape_accuracy`, `overall.perception_color_accuracy` | whether perception recovered the drawn shape class and colour family |
| `overall.mean_naming_recall`, `overall.mean_abstention` | naming on held-out members, and declining on held-out non-members |
| `overall.total_hallucinations` | names given to instances that were not members |
| `overall.ablated_*` | the same measurements with the learned rules removed |
| `overall.model_calls` | language model calls over the whole study |

## `perceive-eval2.json`: scale, supervision, and operating range

149 images taught in one run. Four studies share the file.

| Field | What it carries |
|---|---|
| `scale.per_category` | recall, abstention and false namings for each of eight categories |
| `scale.induced_rules` | the rule recorded for each category, or `None` where more than one hypothesis was retained |
| `data_efficiency` | the same measurements against 1, 2, 3 and 4 labelled positives. The `refused` field at `1` quotes the refusal the substrate returned |
| `supervision` | the same against 0, 1 and 2 discriminating counter-examples, with the rule body induced at each setting |
| `operating_range` | perception under noise, blur, rotation, desaturation, occlusion and apparent size; three stimuli per setting, counting how many were reported at all and how many had the correct shape class and colour family |
| `operating_range.minimum_blob_area` | the minimum reported object area, which is a parameter. `by_radius` gives what the faculty reports at the default of 1% of the frame and at 0.1% |
| `overall.median_ms` | median time to perceive an image, teach what was perceived, induce a rule and name an instance |

## `perceive-ambig-01.json`: naming when the examples do not decide

32 inductions over 416 images, in two arms. In the accidental arm the labelled positives share a size the
category does not require; in the clean arm they do not.

| Field | What it carries |
|---|---|
| `summary.by_arm` | how many inductions in each arm left more than one hypothesis standing, and how many hypotheses on average |
| `conditions[].hypotheses` | every hypothesis the induction retained, as a formula |
| `conditions[].deciding_request` | the case the substrate says would eliminate one of them |
| `conditions[].instances[]` | each held-out instance: its perceived features, whether it is a member, whether it was named live, and what each naming policy would have done with it |
| `summary.policies` | the three policies totalled. `unanimity_live` is the substrate's own behaviour; the other two are counterfactuals computed from the same recorded hypotheses |

## `perceive-ambig-02.json`: closing the ambiguity by asking for a case

The 16 undetermined inductions, resolved two ways, capped at four rounds each.

| Field | What it carries |
|---|---|
| `cases[].targeted` | rounds in which the case named by `deciding_request` was supplied |
| `cases[].random` | rounds in which a randomly drawn stimulus was supplied instead |
| `cases[].*.log[]` | per round: what was supplied, how it was labelled, which hypotheses stood afterwards, and what the substrate asked for next |
| `cases[].*.determined_at` | the round at which a single rule remained, or `null` if the cap was reached |
| `summary` | how many of the 16 each arm closed, and in how many rounds on average |

## Stimuli

`stimuli/` holds the images each study drew, one directory per study. They are flat drawings of one shape
in one colour on white, which is what makes perception, learning and abstention separately measurable. The
`ambig-02` directory also holds the stimulus space the study selected from: every combination of shape,
colour and radius, perceived once so that a case could be chosen by its perceived features rather than by
how it was drawn.
