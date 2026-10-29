# MOT_TbD_BoTSORT

**BoT-SORT** - online multi-object tracking by detection on KITTI-MOTS: 25 detectors + the detections of FairMOT.

- Paper: Aharon et al., 2022; official code: `NirAharon/BoT-SORT`
- Principle: ByteTrack + camera-motion compensation + xywh Kalman state (+ ReID variant)
- **(best)**: the best of the 10 trackers on that detector; last column = that best HOTA.
- Implementation: `common/mot/trackers.py` (`botsort`), re-implemented after the official code, official defaults
  (the class docstring lists every value and every `[Unified]` difference). Causality check: all OK.

### Results (BoT-SORT, official defaults, KITTI-MOTS val)

| detector | HOTA | DetA | AssA | MOTA | IDF1 | IDSW | car | pedestrian | tracker ms | pipeline ms | best tracker on this detector |
|---|---|---|---|---|---|---|---|---|---|---|---|
| cascade_rcnn | 0.609 | 0.565 | 0.660 | 0.626 | 0.736 | 171 | 0.691 | 0.527 | 2.92 | 37.8 | 0.625 |
| faster_rcnn | 0.562 | 0.513 | 0.621 | 0.536 | 0.697 | 199 | 0.668 | 0.456 | 2.98 | 27.9 | 0.582 |
| libra_rcnn | 0.560 | 0.512 | 0.620 | 0.453 | 0.669 | 202 | 0.677 | 0.443 | 3.02 | 29.5 | 0.599 |
| dynamic_rcnn | 0.555 | 0.507 | 0.611 | 0.499 | 0.680 | 194 | 0.667 | 0.443 | 2.97 | 28.0 | 0.579 |
| retinanet | 0.527 | 0.476 | 0.587 | 0.544 | 0.679 | 104 | 0.619 | 0.436 | 2.91 | 24.0 | 0.535 |
| gfl | 0.514 | 0.448 | 0.590 | 0.510 | 0.643 | 59 | 0.620 | 0.407 | 2.84 | 23.6 | 0.522 |
| atss | 0.511 | 0.451 | 0.582 | 0.499 | 0.648 | 92 | 0.619 | 0.402 | 2.91 | 24.6 | 0.527 |
| v6 | 0.505 | 0.444 | 0.580 | 0.511 | 0.644 | 101 | 0.637 | 0.374 | 2.90 | 9.5 | 0.509 |
| tood | 0.495 | 0.433 | 0.566 | 0.479 | 0.615 | 71 | 0.620 | 0.369 | 2.84 | 27.6 | 0.506 |
| fcos | 0.490 | 0.418 | 0.579 | 0.467 | 0.612 | 68 | 0.595 | 0.386 | 2.87 | 24.5 | 0.493 |
| deformable_detr | 0.481 | 0.419 | 0.556 | 0.472 | 0.626 | 107 | 0.581 | 0.381 | 2.86 | 71.1 | 0.482 |
| ppyoloe | 0.480 | 0.428 | 0.543 | 0.478 | 0.601 | 111 | 0.651 | 0.309 | 2.88 | 9.2 | 0.487 |
| x | 0.471 | 0.403 | 0.553 | 0.461 | 0.606 | 100 | 0.624 | 0.317 | 2.86 | 8.3 | 0.478 |
| v9 | 0.460 | 0.384 | 0.555 | 0.440 | 0.574 | 71 | 0.608 | 0.311 | 2.83 | 14.8 | 0.460 |
| v10 | 0.452 | 0.388 | 0.529 | 0.448 | 0.580 | 79 | 0.589 | 0.314 | 2.85 | 10.7 | 0.455 |
| v8 | 0.442 | 0.366 | 0.538 | 0.420 | 0.548 | 80 | 0.607 | 0.276 | 2.81 | 8.1 | 0.443 |
| rtmdet | 0.438 | 0.367 | 0.525 | 0.425 | 0.563 | 43 | 0.602 | 0.274 | 2.83 | 9.0 | 0.465 |
| x2 | 0.435 | 0.359 | 0.531 | 0.409 | 0.557 | 64 | 0.597 | 0.274 | 2.82 | 7.8 | 0.452 |
| v11 | 0.429 | 0.350 | 0.533 | 0.391 | 0.524 | 74 | 0.611 | 0.247 | 2.81 | 9.2 | 0.435 |
| v12 | 0.416 | 0.325 | 0.542 | 0.371 | 0.505 | 62 | 0.585 | 0.246 | 2.82 | 11.3 | 0.424 |
| v13 | 0.365 | 0.294 | 0.476 | 0.333 | 0.431 | 88 | 0.585 | 0.145 | 2.80 | 13.4 | 0.372 |
| v1 | 0.360 | 0.330 | 0.396 | 0.352 | 0.461 | 181 | 0.501 | 0.218 | 2.84 | 8.7 | 0.374 |
| fairmot | 0.353 | 0.275 | 0.456 | 0.331 | 0.463 | 27 | 0.496 | 0.209 | 2.77 | 11.0 | 0.387 |
| centernet | 0.344 | 0.258 | 0.467 | 0.305 | 0.441 | 20 | 0.487 | 0.202 | 4.36 | 11.9 | 0.395 |
| v26 | 0.337 | 0.278 | 0.424 | 0.322 | 0.410 | 57 | 0.580 | 0.094 | 2.80 | 11.6 | 0.390 |
| ssd | **0.288** (best) | 0.254 | 0.346 | 0.292 | 0.356 | 68 | 0.555 | 0.021 | 2.77 | 32.1 | 0.288 |

### Score-threshold sensitivity (BoT-SORT, HOTA with one common threshold)

| detector | 0.3 | 0.4 | 0.5 | 0.6 | 0.7 |
|---|---|---|---|---|---|
| deformable_detr | 0.510 | 0.505 | 0.500 | 0.481 | 0.429 |
| faster_rcnn | 0.535 | 0.543 | 0.552 | 0.562 | 0.570 |
| fcos | 0.532 | 0.539 | 0.521 | 0.490 | 0.436 |
| libra_rcnn | 0.541 | 0.550 | 0.558 | 0.560 | 0.572 |
| ppyoloe | 0.495 | 0.509 | 0.506 | 0.480 | 0.433 |
| rtmdet | 0.510 | 0.504 | 0.487 | 0.438 | 0.349 |
| v10 | 0.506 | 0.501 | 0.488 | 0.452 | 0.387 |
| v11 | 0.489 | 0.484 | 0.465 | 0.429 | 0.360 |
| v12 | 0.485 | 0.480 | 0.460 | 0.416 | 0.275 |
| v13 | 0.413 | 0.408 | 0.392 | 0.365 | 0.296 |
| v26 | 0.452 | 0.443 | 0.421 | 0.337 | 0.252 |
| v6 | 0.530 | 0.541 | 0.527 | 0.505 | 0.471 |
| v8 | 0.491 | 0.491 | 0.474 | 0.442 | 0.380 |
| v9 | 0.490 | 0.483 | 0.472 | 0.460 | 0.385 |
| x | 0.485 | 0.484 | 0.481 | 0.471 | 0.401 |
| x2 | 0.487 | 0.486 | 0.475 | 0.435 | 0.367 |

**BoT-SORT-ReID** - online multi-object tracking by detection on KITTI-MOTS: 25 detectors + the detections of FairMOT.

- Paper: Aharon et al., 2022; official code: `NirAharon/BoT-SORT`
- Principle: BoT-SORT with appearance features (shared ReID)
- **(best)**: the best of the 10 trackers on that detector; last column = that best HOTA.
- Implementation: `common/mot/trackers.py` (`botsort_reid`), re-implemented after the official code, official defaults
  (the class docstring lists every value and every `[Unified]` difference). Causality check: all OK.

### Results (BoT-SORT-ReID, official defaults, KITTI-MOTS val)

| detector | HOTA | DetA | AssA | MOTA | IDF1 | IDSW | car | pedestrian | tracker ms | pipeline ms | best tracker on this detector |
|---|---|---|---|---|---|---|---|---|---|---|---|
| cascade_rcnn | 0.612 | 0.569 | 0.663 | 0.627 | 0.739 | 166 | 0.691 | 0.534 | 3.01 | 40.4 | 0.625 |
| libra_rcnn | 0.578 | 0.515 | 0.658 | 0.456 | 0.695 | 193 | 0.681 | 0.475 | 3.12 | 32.2 | 0.599 |
| faster_rcnn | 0.568 | 0.514 | 0.634 | 0.539 | 0.702 | 188 | 0.667 | 0.469 | 3.08 | 30.8 | 0.582 |
| dynamic_rcnn | 0.561 | 0.509 | 0.623 | 0.502 | 0.693 | 179 | 0.670 | 0.453 | 3.06 | 31.0 | 0.579 |
| retinanet | **0.535** (best) | 0.480 | 0.600 | 0.545 | 0.689 | 98 | 0.621 | 0.450 | 2.96 | 27.9 | 0.535 |
| gfl | 0.521 | 0.451 | 0.602 | 0.512 | 0.649 | 54 | 0.620 | 0.421 | 2.92 | 27.0 | 0.522 |
| atss | 0.519 | 0.455 | 0.595 | 0.503 | 0.658 | 88 | 0.619 | 0.419 | 3.01 | 42.2 | 0.527 |
| v6 | **0.509** (best) | 0.446 | 0.585 | 0.513 | 0.649 | 94 | 0.638 | 0.381 | 2.97 | 13.8 | 0.509 |
| tood | 0.503 | 0.434 | 0.585 | 0.481 | 0.628 | 68 | 0.620 | 0.386 | 2.92 | 31.8 | 0.506 |
| fcos | **0.493** (best) | 0.421 | 0.581 | 0.469 | 0.613 | 63 | 0.595 | 0.391 | 2.93 | 36.7 | 0.493 |
| ppyoloe | 0.484 | 0.429 | 0.551 | 0.479 | 0.606 | 107 | 0.650 | 0.318 | 2.95 | 14.7 | 0.487 |
| deformable_detr | **0.482** (best) | 0.419 | 0.557 | 0.472 | 0.627 | 108 | 0.581 | 0.382 | 2.94 | 74.5 | 0.482 |
| x | **0.478** (best) | 0.407 | 0.566 | 0.464 | 0.619 | 89 | 0.625 | 0.332 | 3.16 | 11.6 | 0.478 |
| v9 | **0.460** (best) | 0.384 | 0.555 | 0.440 | 0.575 | 70 | 0.609 | 0.311 | 2.89 | 16.8 | 0.460 |
| v10 | **0.455** (best) | 0.389 | 0.537 | 0.448 | 0.585 | 78 | 0.597 | 0.314 | 2.92 | 13.5 | 0.455 |
| rtmdet | 0.444 | 0.369 | 0.539 | 0.425 | 0.571 | 43 | 0.602 | 0.286 | 2.90 | 12.7 | 0.465 |
| v8 | **0.443** (best) | 0.366 | 0.540 | 0.421 | 0.549 | 79 | 0.607 | 0.278 | 3.10 | 11.0 | 0.443 |
| x2 | 0.440 | 0.360 | 0.539 | 0.411 | 0.562 | 60 | 0.597 | 0.282 | 2.89 | 13.7 | 0.452 |
| v11 | 0.429 | 0.350 | 0.533 | 0.391 | 0.524 | 74 | 0.611 | 0.247 | 2.88 | 11.8 | 0.435 |
| v12 | 0.416 | 0.325 | 0.543 | 0.371 | 0.505 | 62 | 0.585 | 0.246 | 2.87 | 14.2 | 0.424 |
| v13 | 0.365 | 0.293 | 0.478 | 0.331 | 0.432 | 87 | 0.584 | 0.145 | 2.87 | 16.1 | 0.372 |
| v1 | 0.364 | 0.331 | 0.405 | 0.354 | 0.469 | 169 | 0.503 | 0.226 | 2.98 | 11.4 | 0.374 |
| fairmot | 0.354 | 0.275 | 0.459 | 0.331 | 0.466 | 26 | 0.496 | 0.211 | 3.04 | 11.3 | 0.387 |
| centernet | 0.344 | 0.258 | 0.467 | 0.305 | 0.441 | 20 | 0.487 | 0.202 | 3.37 | 15.4 | 0.395 |
| v26 | 0.337 | 0.278 | 0.424 | 0.322 | 0.411 | 57 | 0.580 | 0.094 | 2.86 | 14.6 | 0.390 |
| ssd | 0.287 | 0.254 | 0.344 | 0.292 | 0.354 | 68 | 0.552 | 0.021 | 3.06 | 35.0 | 0.288 |

### Score-threshold sensitivity (BoT-SORT-ReID, HOTA with one common threshold)

| detector | 0.3 | 0.4 | 0.5 | 0.6 | 0.7 |
|---|---|---|---|---|---|
| deformable_detr | 0.513 | 0.511 | 0.503 | 0.482 | 0.431 |
| faster_rcnn | 0.536 | 0.546 | 0.559 | 0.568 | 0.573 |
| fcos | 0.540 | 0.542 | 0.523 | 0.493 | 0.438 |
| libra_rcnn | 0.526 | 0.556 | 0.563 | 0.578 | 0.582 |
| ppyoloe | 0.501 | 0.517 | 0.508 | 0.484 | 0.436 |
| rtmdet | 0.520 | 0.513 | 0.494 | 0.444 | 0.351 |
| v10 | 0.515 | 0.506 | 0.493 | 0.455 | 0.390 |
| v11 | 0.498 | 0.485 | 0.465 | 0.429 | 0.360 |
| v12 | 0.499 | 0.491 | 0.469 | 0.416 | 0.275 |
| v13 | 0.417 | 0.408 | 0.392 | 0.365 | 0.296 |
| v26 | 0.460 | 0.447 | 0.421 | 0.337 | 0.252 |
| v6 | 0.537 | 0.543 | 0.532 | 0.509 | 0.476 |
| v8 | 0.495 | 0.492 | 0.478 | 0.443 | 0.380 |
| v9 | 0.504 | 0.495 | 0.483 | 0.460 | 0.385 |
| x | 0.486 | 0.488 | 0.485 | 0.478 | 0.402 |
| x2 | 0.498 | 0.499 | 0.483 | 0.440 | 0.373 |

Part of the *Physical AI MOT* comparison of the **Statera Working Group**: 10 trackers x 25 detectors (+ the detections of FairMOT), 3 joint
detection-and-tracking networks and 1 end-to-end tracker under one protocol. The full comparison (Pareto front,
tracker ranking, JDT / E2E against tracking-by-detection) is in `MOT_Detectors_KITTIMOTS` (`RESULTS.md`).

## Protocol (all MOT_* repositories)

- Online / causal only: every method sees the current frame and its own state; checked by re-running prefixes of
  every sequence (the output of frame t must not change when later frames are removed).
- Input 1216 x 384 (KITTI 1242 x 375 letterboxed), detectors trained from scratch on KITTI-MOTS train (12 sequences),
  30 epochs, Adam 1e-4, effective batch 8, seed 777 - the protocol of the *Physical AI Object Detection* series.
- Metrics: HOTA / DetA / AssA (TrackEval classes, car / pedestrian mean), MOTA, IDF1, IDSW.
- Latency: RTX 4070 Laptop GPU, batch 1, fp32, medians over val; pipeline = detector (forward + post-processing) +
  ReID (appearance trackers) + tracker (CPU); image decoding / letterboxing not included.
- Trackers run with their official default parameters; frame-based values given for 30 fps are scaled to 10 fps.
  A sensitivity table with one common score threshold for every tracker is reported separately (chosen on val, so it
  is analysis, not ranking).

## Data: KITTI-MOTS (box level, val = 9 sequences, 2,981 frames)

KITTI tracking images (21 training sequences) with instance / track annotations; boxes = tight boxes of the masks,
classes car and pedestrian, ignore regions (id 10000) neither rewarded nor penalised. The annotations are taken from
the **KITTI-STEP** panoptic maps (same sequences and split, car / person instances merged from KITTI-MOTS; frames,
track counts and pedestrian masks match the KITTI-MOTS paper, car masks differ by 39 of 26,899).

```bash
bash tools/mot/get_kitti_mots.sh            # KITTI tracking images + annotations (KITTI-STEP fallback)
python tools/mot/kittimots_to_voc.py        # VOC-layout copy with tracks + count report
UNIFIED_IMAGE_DATASET=kittimots python tools/mot/count_loader.py     # counts as the loaders read them
```

**Licence of the data and of every trained weight here: KITTI / KITTI-MOTS / KITTI-STEP are CC BY-NC-SA 3.0
(non-commercial).**

## Usage

```bash
pip install -r requirements.txt
pip install "git+https://github.com/JonathonLuiten/TrackEval.git@12c8791b303e0a0b50f753af204249e622d0281a"
# saved detections (+ ReID features) of the 25 detectors: Release of Statera-Workshop/MOT_Detectors_KITTIMOTS
python tools/mot/run_tracker.py --source kittimots --dets dets/x_reid.npz --trackers botsort botsort_reid --causal
python tools/mot/run_tracker.py --source kittimots --dets dets/x_reid.npz --gt-as-pred      # evaluation self-test
python tools/mot/mot_table.py                                                             # tables of all runs
```

`run_tracker.py --trackers` accepts every tracker of the comparison (iou, sort, bytetrack, ocsort, hybridsort, botsort, botsort_reid, deepsort, tracktrack, fairmot), so other
trackers can be run on the same detections. Results of this repository: `results/` (JSON per detector).

## Files

```
common/mot/trackers.py    the trackers of the comparison (default here: botsort)
common/mot/core.py        boxes, IoU, assignment, Kalman filters, camera-motion estimation
common/mot/evaluate.py    KITTI-MOTS ground truth and TrackEval metrics
tools/mot/run_tracker.py  run / time / evaluate trackers on saved detections (+ causality check)
tools/mot/*kitti*         data preparation
results/                  evaluation JSON of this repository's tracker(s)
THIRD_PARTY.md            sources and licences
```

## Global Collaboration

Hills Robotics is currently participating in multiple projects in Korea and internationally.

We are actively interested in building relationships with organizations that can complement our technology with global sales networks, distribution channels, system integration capabilities, manufacturing ecosystems, AI infrastructure, robotics technologies, research capabilities, or strategic investment.

Several technology and business collaborations are already underway. Some partners, projects, system architectures, and commercial programs cannot be publicly disclosed because they are subject to confidentiality and business agreements.

We believe that the emerging Physical AI ecosystem cannot be built by a single company.
It requires a global network connecting robotics companies, AI researchers, semiconductor and computing companies, sensor manufacturers, software developers, universities, system integrators, industrial customers, investors, and global distribution partners.

We have now begun our serious exploration of the Physical AI frontier, and we welcome connections with people and organizations who want to build this ecosystem together.

## Research, Contribution, and Donation

The repositories of the Statera Working Group are intended to contribute to the broader technical discussion around Physical AI.

Researchers, engineers, developers, companies, universities, and independent contributors interested in these subjects are welcome to connect with us.

If you would like to collaborate on Physical AI or autonomous robotics, participate in research or technology development, discuss international business cooperation, propose technology or platform integration, contribute technical knowledge, or support this GitHub knowledge initiative through sponsorship or donation, please contact us.

## Contact

**Richard Minsoo Go**
Head of AI, Hills Robotics
Statera Working Group

Personal / Research Contact:
[gominsoo888@gmail.com](mailto:gominsoo888@gmail.com)

Hills Robotics / Business Contact:
[minsoo.go@hillslogis.com](mailto:minsoo.go@hillslogis.com)

Hills Robotics:
https://hillslogis.com/

For inquiries regarding next-generation outdoor autonomous robotic platforms, Physical AI Spider Grid, Intelligence Cabinet, Edge AI, or On-Premise AI architectures that are not yet publicly presented on the company website, please contact us directly.
