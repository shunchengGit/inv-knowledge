---
type: 行业研报
title: 行业研究-AI - Jefferies Huaweis Tau Scaling Law Not Yet a DeepSeek Moment for C...
description: China (PRC) | Technology
timestamp: 2026-06-23T23:32:08.278661+08:00
resource: res/行业研究-AI/2026-05-28-Jefferies-Huaweis _Tau_ Scaling Law - Not Yet a DeepSeek Moment for C...-122278601.pdf
source_type: pdf
tags: [行业研究-AI, 行业分析, 新鲜]
---

### 2026-05-28-Jefferies-Huaweis _Tau_ Scaling Law - Not Yet a DeepSeek Moment for C...-122278601.pdf  (总页数=12)

--- 第1页 ---
China (PRC) | Technology
Equity Research
May 28, 2026
 
Nick Cheng *  | Equity Analyst
+852 3743 8750 | nick.cheng@jefferies.com
Edison Lee, CFA *  | Equity Analyst
852 3743 8009 | edison.lee@jefferies.com
Jacky He *  | Equity Analyst
+852 3743 8084 | jacky.he@jefferies.com
Matt Ma *  | Equity Analyst
852 3767 1109 | matt.ma@jefferies.com
Annie Ping, CFA, FRM *  | Equity Associate
+852 3767 1273 | annie.ping@jefferies.com
Huawei's "Tau" Scaling Law - Not Yet a
DeepSeek Moment for China Semi
Huawei's top-down system topology aims at making chips without EUV
that could perform like 1.4nm chips (2031). One key is Logic Folding,
which connects two chips using hybrid bonding as a routing resource. This
could reduce die size (potentially higher yield) and shorten transmission
distance (higher performance). But we see challenges in heat dissipation,
wafer variations, hybrid bonding density and more. Positive for EDA, WFE,
foundries and optics.
Huawei’s (HW) τ Scaling Law reframes chip performance from node-based scaling to
system-level time optimization. Presented at ISCAS 2026, Huawei’s τ / Tau Scaling Law shifts
focus from traditional geometry scaling / Moore’s Law toward a holistic, top-down design
methodology. Instead of treating process node size, such as “x nm,” as the primary proxy
for performance, HW argues that time-to-computation / τ should become the key metric.
Performance gains can come not only from transistor shrink, but also from circuit design,
chip architecture, packaging, interconnect, and system-level optimization. This roadmap is
especially relevant as Moore’s Law slows and Huawei faces restricted access to leading-edge
process technologies.
Logic Folding is HW’s most notable example of using 3D design to reduce critical-path
delay. In chip design, performance is capped by the slowest signal path, known as the critical
path. Traditionally, engineers shorten this path through better place-and-route or by moving to
a more advanced process node. HW’s Logic Folding concept attempts to “fold” a 2D chip layout
into a 3D structure by stacking logic layers, allowing connected elements to be placed closer
together vertically. Although this resembles existing 3D-IC and chiplet approaches, HW’s vision
is more integrated: instead of treating chiplets as separate black boxes connected through
limited I/O, Logic Folding aims to co-optimize multiple layers as one unified design.
Full Logic Folding could create major opportunities, but it faces significant technical
challenges. The roadmap can be viewed in three stages: basic 3D stacking (ie, 3D-IC proposed
by TSMC/Intel), co-simulation-level Logic Folding, and ultimately co-design-level Logic Folding.
The most advanced stage would require EDA tools to treat hybrid-bonding layers as routing
resources, effectively moving chip design from 2D into true 3D. This would require a major
redesign of the EDA toolchain and create demand for 3D-aware place-and-route, timing,
thermal, and reliability tools. However, major obstacles remain, including overheating, wafer-to-
wafer variation, limited hybrid-bonding density, TSV reliability, yield risk, and manufacturability.
As a result, full commercial viability may take a long time.
We examine how this roadmap would impact different supply chain players. HW also
extends τ scaling beyond chips through its System-as-One-Chip concept, using Unified Bus
and Hi-ONE optical interconnects to optimize the entire AI system. This could simplify data-
center architecture, reduce latency, improve heat dissipation, and lower total cost of ownership
by replacing fragmented protocols with a more unified topology. If successful, the roadmap
could benefit EDA vendors (higher demand but needs innovations), hybrid bonding equipment
suppliers, optical interconnect players, and advanced node foundries. However, it could
pressure AI server ODMs (simplified configuration), cooling (reduced demand) and power
suppliers (lower power density), and independent Chinese AI chip design houses, if HW gains a
proprietary system-level performance advantage. This roadmap will likely have global impact,
as non-Chinese players could also pursue this approach and geometry scaling simultaneously.
Chart 1 - Bottom-up System Design
.
Source: Jefferies
Chart 2 - Space Folding
.
Source: Jefferies
Chart 3 - Core Concept of τ (Tau) Scaling
.
Source: Jefferies
Chart 4 - Face to Face Hybrid Bonding
.
Source: Jefferies
 
Please see analyst certifications, important disclosure information, and information regarding the status of non-US analysts on pages  7 - 12 of this report.
 * Jefferies Hong Kong Limited
--- 第2页 ---
Technology
Equity Research
May 28, 2026
 
On 2026 May 25, Huawei presented “τ (Tau) Scaling Law” at the IEEE International Symposium
on Circuits and Systems (ISCAS) 2026. The company turned their design strategy to a more
holistic/top-down approach from a bottom up/lego-like approach, which the industry has
been using for decades. The change/innovation is more on design methodology rather than
manufacturing technologies, so it offers the industry a way to pursue better performance without
accessing the latest process node tech. Although there are still technological challenges to
overcome, the proposal already made a “dimensional” impact on computing, including AI, system
design.
 
Chart 5 - τ (Tau) Scaling
.
Source: Jefferies
 
 
Chart 6 - Core Concept of τ (Tau) Scaling
.
Source: Jefferies
 
 
 
Huawei first proposed “τ scaling” as the new metric to replace traditional “geometry scaling/
Moore’s law” to evaluate a new system. It is because while geometry scaling can lead to
computing performance gain, it is not the only factor. Device shrink (geometry scaling), circuit
design, chip design and system design improvement can all improve the performance of a compute
system. From Huawei’s perspective, as Moore’s law slows down, geometry shrink will create less
incremental performance gain, so geometry scaling (such as x nm) can no longer be used as the
only proxy of performance. They believe time, which shows how fast a computation can be done,
should be the new metric of evaluating systems performance.
 
 
This concept is not entirely new. Due to geopolitical tension, Huawei has been trying to use
better system design to overcome US restrictions that constrain their chip performance. However,
in IC design, chip performance is usually balanced against other requirements, such as power
efficiency, heat control, cost, reliability, and many more We believe Huawei, as one of the best chip
design houses globally, clearly understands that. Thus, we see the announcement of this “τ Scaling”
roadmap a declaration that Huawei would pursue higher chip performance at all costs.
 
In the presentation, Huawei used some examples to demonstrate how this new roadmap will be
executed. Among all the examples, “Logic-folding” is the most eye-catching one.
Sci-Fi fans must be familiar with “space folding” and “wormhole”. A typical demonstration for space
folding is to draw two points on a paper. On a 2-dimensional paper, the closest distance of the
two points is the straight line between the two. However, in a 3-dimensional space, the paper can
be folded so the two points overlap each other and the distance between them is practically zero.
When moving from a lower dimension world to a higher one, space can be folded, and distance
can be shortened.
 
 
Please see important disclosure information on pages 7 - 12 of this report.
This report is intended for Jefferies clients only. Unauthorized distribution is prohibited.
2
--- 第3页 ---
Technology
Equity Research
May 28, 2026
 
Chart 7 - Space Folding
.
Source: Jefferies
 
 
Chip-performance is capped by the slowest part of the chip, which is determined by the distance
between two connected transistors (because signal's travel time will be longer for longer distance).
The industry's term for the longest connection is “critical path”. In other words, if engineers can
shorten the “critical path”, they can boost the performance of the chip. Traditionally, this can be
achieved by:
1.
Optimizing Place & Route (P&R): It means cleverly placing all related transistors closer to
each other to minimize critical path. This is one of the most critical functions of EDA tools.
2.
Using more advanced node manufacturing tech: transistor size and wire lengths among them
naturally shrink as the chip migrates to more advanced node. In consequence, critical path
also naturally shortens.
 
Both methods aim to shorten critical paths in a two-dimensional (2D) space because modern
“chip” design is essentially a 2D design, where all transistors are placed on the same surface. If
engineers have already done their best in P&R, traditionally, the only way to improve further is to
adopt more advanced node. Therefore, the industry sees geometry scaling the proxy and metric of
chip performance improvement.
 
With the holistic approach, Huawei argues that design engineers should only focus on the “end
performance (τ)” instead of geometry scaling, which is just one of the factors that might lead to
better performance. They transformed the 2D space in a chip into a three-dimensional (3D) space
by stacking one chip on top of another. Just like folded paper we discussed above, the space is
folded, and the longest distance (critical path) is shortened. Hence the performance (τ) increases
without any change in geometry scale.
 
For many tech investors, this may sound very similar to the 3D-IC concept that TSMC and Intel
proposed long time ago. However, there are some significant differences.
An analogy for the differences is connecting two apartment units with one directly above the other
to create a duplex. If you ask two interior design teams to work on each unit separately, there
would be some redundancies and suboptimal design between the two units. If a single team takes
a holistic view to design the entire duplex, the team will likely be able to utilize the entire space more
efficiently by, for example, putting all bedrooms upstairs, and creating a bigger living room and also
a bigger kitchen downstairs.
 
TSMC’s current chip-let/3D-IC approach is similar to the first approach. Each chip-let is self-
optimized within its own and use very limited I/O ports to communicate with other chip-lets. In other
words, TSMC's job is only to build a staircase to connect the two floors. Each floor is designed
by separate teams with possibly different objectives. However, Huawei wants to design the entire
duplex with a unified approach and style
 
 
Please see important disclosure information on pages 7 - 12 of this report.
This report is intended for Jefferies clients only. Unauthorized distribution is prohibited.
3
--- 第4页 ---
Technology
Equity Research
May 28, 2026
 
We see three levels of 3D chip design:
1. 3D Stacking (Current TSMC's SoIC solutions)
a. Each chip-let is a black box. Design engineers only know the I/O information about the chip.
The benefit of this is to allow multiple companies' IPs to co-exist in the same 3D chip.
b. This is the least integrated solution.
Chart 8 - 3D Stacking
.
Source: Jefferies
 
2. Co-simulation-level Logic Folding*
a. The box needs to share its model (gate level design Information) so that the other chip may
use this information to identify critical path.
b. EDA tools still do the simulation separately in 2D chips and then optimize by identifying and
shortening critical paths via vertical connections.
c. This approach is less likely to allow collaboration as no design houses want to share their
models (gate level design information), which are considered commercial secrets.
d. The existing EDA tools already can achieve this. TSMC already provides PDK and EDA vendors
use TSMC's PDK to simulate TSV and related circuit. According to Huawei’s paper, we believe
they are at this stage
…(截断)
