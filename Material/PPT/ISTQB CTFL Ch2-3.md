<!-- Slide 1 -->

2. 在整个软件开发生命周期中进行测试 – 130 分钟


---

<!-- Slide 2 -->

关键字
验收测试， 黑盒测试， 组件集成测试， 组件测试，
确认测试， 功能测试， 集成测试， 维护测试，
非功能测试， 回归测试， 左移， 系统集成测试， 系统测试，
测试级别， 测试对象， 测试类型， 白盒测试
2

---

<!-- Slide 3 -->

第 2 章的学习目标：
2.1 在软件开发生命周期的上下文中进行测试
FL-2.1.1  （K2）解释所选软件开发生命周期对测试的影响
FL-2.1.2 （K1）回顾适用于所有软件开发生命周期的良好测试实践
FL-2.1.3 （K1）回顾测试优先的开发方法示例
FL-2.1.4 （K2）总结 DevOps 对测试有何影响
FL-2.1.5 （K2）解释左移
FL-2.1.6 （K2）解释如何将回顾用作流程改进的机制
2.2 测试级别和测试类型
FL-2.2.1 （K2）区分不同的测试级别
FL-2.2.2 （K2）区分不同的测试类型
FL-2.2.3 （K2）区分确认测试与回归测试
2.3 维护测试
FL-2.3.1 （K2）总结维护测试及其触发因素
3

---

<!-- Slide 4 -->

2.1. 在软件开发生命周期 （SDLC） 的上下文中进行测试
SDLC 模型是软件开发过程的抽象、高级表示。
SDLC 模型定义了在此过程中执行的不同开发阶段和活动类型在逻辑和时间上如何相互关联。
SDLC 模型的示例包括：
顺序开发模型（例如，瀑布模型、V 模型）
迭代开发模型（例如，螺旋模型、原型设计）
增量开发模型（例如，统一流程）
4

---

<!-- Slide 5 -->

2.1. 在软件开发生命周期 （SDLC） 的上下文中进行测试 (cont.)
软件开发过程中的某些活动也可以通过更详细的软件开发方法和敏捷实践来描述。示例包括：
验收测试驱动开发 （ATDD）
行为驱动开发 （BDD）
领域驱动设计 （DDD）
极限编程 （XP）
功能驱动开发 （FDD）
Kanban
Lean IT
Scrum
测试驱动开发 （TDD）。

5

---

<!-- Slide 6 -->

2.1.1. 	软件开发生命周期对测试的影响
测试必须适应 SDLC 才能成功。
SDLC 的选择会影响：
测试活动的范围和时间（例如，测试级别和测试类型）
测试文档的详细程度
测试技术和测试方法的选择
测试自动化程度
测试人员的角色和职责
6

---

<!-- Slide 7 -->

2.1.1. 	软件开发生命周期对测试的影响 (cont.)
**在顺序开发模型中，在初始阶段，测试人员通常参与需求审查、测试分析和测试设计。可执行代码通常是在后期阶段创建的，因此通常不能在 SDLC 的早期执行动态测试。**
**在一些迭代开发模型和增量开发模型中，假设每次迭代都提供一个工作原型或产品增量。这意味着在每次迭代中，静态测试和动态测试都可以在所有测试级别执行。频繁交付增量需要快速反馈和广泛的回归测试。**
敏捷软件开发假设整个项目可能会发生更改。因此，轻量级工作产品文档和广泛的测试自动化使回归测试更容易，在敏捷项目中受到青睐。此外，大多数手动测试往往使用基于经验的测试技术（参见第 4.4 节）完成，这些技术不需要大量的事先测试分析和设计。

7

---

<!-- Slide 8 -->

Question #A7
You are working as a tester in the team that follows the V-model. Which of the following activities CAN be performed in the initial phases of the SDLC?
a) Dynamic test execution
b) Static testing
c) Test planning
d) Acceptance test execution
e) Maintenance testing
#### Select TWO options.
8

---

<!-- Slide 9 -->

2.1.2. 	软件开发生命周期和良好测试实践
与所选的 SDLC 模型无关的良好测试实践包括以下内容：
对于每个软件开发活动，都有相应的测试活动，因此所有开发活动都受到质量控制
不同的测试级别（参见第 2.2.1 章）具有特定和不同的测试目标，这使得测试在避免冗余的同时具有适当的全面性
给定测试级别的测试分析和设计在 SDLC 的相应开发阶段开始，以便测试可以遵循早期测试的原则（参见第 1.3 节）
一旦这些工作产品的草稿可用，测试人员就会参与审查工作产品，以便早期的测试和缺陷检测可以支持左移（参见第 2.1.5 节）。
9

---

<!-- Slide 10 -->

Question #9
Consider the following rule: “for every SDLC activity there is a corresponding test activity”. In which SDLC models does this rule hold?
a) Only in sequential SDLC models
b) Only in iterative SDLC models
c) Only in iterative and incremental SDLC models
d) In sequential, incremental, and iterative SDLC models


10

---

<!-- Slide 11 -->

2.1.3. 	作为软件开发的驱动因素进行测试
TDD、ATDD 和 BDD 是类似的开发方法，其中测试被定义为指导开发的一种手段。这些方法中的每一种都实现了早期测试的原则（参见 1.3 节）并遵循左移（参见 2.1.5 节），因为测试是在编写代码之前定义的。它们支持迭代开发模型。
测试驱动开发 （TDD）：
通过测试用例（而不是广泛的软件设计）指导编码 （Beck 2003）
首先编写测试，然后编写代码以满足测试，然后重构测试和代码
验收测试驱动开发 （ATDD）（参见 4.5.3 节）：
作为系统设计过程的一部分，从验收标准中得出测试 （Gärtner 2011）
为了满足测试，在开发应用程序的某一部分之前编写测试
行为驱动开发 （BDD）：
通过以简单的自然语言形式编写的测试用例来表达应用程序的期望行为，利益相关者很容易理解 - 通常使用 Given/When/Then 格式 （Chelimsky 2010）
然后，测试用例应自动转换为可执行测试
对于上述所有方法，测试可能会作为自动化测试持续存在，以确保将来调整/重构的代码质量。
11

---

<!-- Slide 12 -->

Question #10
Which of the following statements BEST describes the acceptance test-driven development (ATDD) approach?
a) In ATDD, acceptance criteria are typically created based on the given/when/then format
b) In ATDD, test cases are mainly created at component testing and are code-oriented
c) In ATDD, tests are created, based on acceptance criteria to drive the development of the related software
d) in ATDD, tests are based on the desired behavior of the software, which makes it easier for team members to understand them

12

---

<!-- Slide 13 -->

2.1.4. 	DevOps 和测试
DevOps 是一种组织方法，旨在通过让开发（包括测试）和运营协同工作来实现一系列共同目标，从而产生协同效应。
DevOps 需要在组织内部进行文化转变，以弥合开发（包括测试）和运营之间的差距，同时以同等价值对待它们的功能。
## DevOps 促进团队自主、快速反馈、集成工具链以及持续集成 （CI, continuous integration） 和持续交付 （CD, continuous delivery） 等技术实践。这使团队能够通过 DevOps 交付管道更快地构建、测试和发布高质量代码 （Kim 2016）。
13

---

<!-- Slide 14 -->

2.1.4. 	DevOps 和测试 (cont.)
从测试的角度来看，DevOps 的一些好处如下：
代码质量的快速反馈，以及更改是否对现有代码产生不利影响
CI 通过鼓励开发人员提交高质量的代码并附有组件测试和静态分析来促进测试中的左移（参见第 2.1.5 节）
像 CI/CD 一样推广自动化流程，这有助于建立稳定的测试环境
对非功能性质量特征的可见性增加（例如，性能效率、 可靠性）
通过交付管道实现自动化，减少了重复手动测试的需求
由于自动化回归测试的规模和范围，回归风险被降至最低
DevOps 并非没有风险和挑战，其中包括：
必须定义和建立 DevOps 交付管道
必须引入和维护 CI/CD 工具
测试自动化需要额外的资源，并且可能难以建立和维护
尽管 DevOps 具有高水平的自动化测试，但仍需要手动测试（尤其是从用户的角度来看）。

14

---

<!-- Slide 15 -->

Question #A8
Which of the following are advantages of DevOps?
i) Faster product release and faster time to market
ii) Increases the need for repetitive manual testing
iii) Constant availability of executable software
iv) Reduction in the number of regression tests associated with code refactoring
v) Setting up the test automation framework is inexpensive since everything is automated
a) i, ii, iv are advantages
b) iii, v are advantages
c) i, iii are advantages
d) ii, iv, v are advantages

15

---

<!-- Slide 16 -->

2.1.5. 	左移
早期测试的原则（参见第 1.3 节）有时被称为左移，因为它是一种在 SDLC 中较早执行测试的方法。左移基本上意味着应该更早地进行测试（例如，不要等待代码实现或组件集成），但这并不意味着应该忽略 SDLC 中的后期测试。
有一些良好的实践说明了如何在测试中实现“左移”，其中包括：
从测试人员的角度审查规范。这些规范审查活动通常会发现潜在的缺陷，例如歧义、不完整和不一致
在编写代码之前编写测试用例，并在代码实现期间让代码在测试框架中运行
使用 CI 甚至更好的 CD，因为它带有快速反馈和自动化组件测试，以便可以随同源代码提交到代码存储库
在动态测试之前完成源代码的静态分析，或作为自动化过程的一部分
尽可能从组件测试级别开始执行非功能测试。这是一种左移形式，因为当完整的系统和代表性测试环境可用时，这些非功能性测试类型往往会在 SDLC 中稍后执行
左移可能会导致在流程早期产生额外的培训、努力和/或成本，但预计会在流程后期节省精力和/或成本。
对于左移，重要的是让利益相关者相信并接受这个概念。
16

---

<!-- Slide 17 -->

Question #11
Which of the following is NOT an example of the shift left approach?
a) Reviewing the user requirements before they are formally accepted by the stakeholders
b) Writing a component test before the corresponding code is written
c) Executing a performance efficiency test for a component during component testing
d) Writing a test script before setting up the configuration management process

17

---

<!-- Slide 18 -->

2.1.6. 	回顾和流程改进
回顾通常在项目或迭代结束时、发布里程碑举行，或者可以在需要时举行。回顾的时间安排和组织取决于所遵循的特定 SDLC 模型。在这些会议中，参与者（不仅是测试人员，还包括开发人员、架构师、产品所有者、业务分析师）讨论：
什么是成功的，应该保留的？
哪些方面没有成功，哪些地方可以改进？
如何整合改进并在将来保持成功？
结果应被记录下来，并且通常是测试完成报告的一部分（参见第 5.3.2 节）。回顾对于成功实施持续改进至关重要，并且跟进任何建议的改进都很重要。
测试的典型好处包括：
提高测试效果/效率（例如，通过实施流程改进建议）
提高测试件的质量（例如，通过共同审查测试流程）
团队凝聚力和学习（例如，由于有机会提出问题和提出改进点）
提高测试基础的质量（例如，可以解决和解决需求范围和质量方面的缺陷）
开发和测试之间更好的合作（例如，定期审查和优化协作）
18

---

<!-- Slide 19 -->

Question #12
Which of the arguments below would you use to convince your manager to organize retrospectives at the end of each release cycle?
a) Retrospectives are very popular these days and clients would appreciate it if we added them to our processes
b) Organizing retrospectives will save the organization money because without them end user representatives do not provide immediate feedback about the product
c) Process weaknesses identified during the retrospective can be analyzed and serve as a to do list for the organization’s continuous process improvement program
d) Retrospectives embrace five values including courage and respect, which are crucial to maintain continuous improvement in the organization


19

---

<!-- Slide 20 -->

2.2. 测试级别和测试类型
测试级别是一起组织和管理的测试活动组。每个测试级别都是测试过程的一个实例，在给定的开发阶段与软件相关执行，从单个组件到整个系统，或者在适用的情况下，从系统系统。
测试级别与 SDLC 中的其他活动相关。在顺序 SDLC 模型中，通常定义测试级别，以便一个级别的退出标准是下一个级别的进入标准的一部分。在某些迭代模型中，这可能不适用。开发活动可能跨越多个测试级别。测试级别可能在时间上重叠。
测试类型是与特定质量特征相关的测试活动组，其中大多数测试活动都可以在每个测试级别执行。
20

---

<!-- Slide 21 -->

2.2.1. 	测试级别
**组件测试 （也称为单元测试） 侧重于孤立地测试组件。它通常需要特定的支持，例如测试工具或单元测试框架。组件测试通常由开发人员在其开发环境中执行。**
**组件集成测试 （也称为单元集成测试）侧重于测试组件之间的接口和交互。组件集成测试在很大程度上依赖于集成策略，如自下而上、自上而下或大爆炸。**
系统测试 侧重于整个系统或产品的整体行为和功能，通常包括端到端任务的功能测试和质量特征的非功能测试。对于一些非功能性质量特征，最好在具有代表性的测试环境中（例如，可用性）的完整系统上对其进行测试。也可以使用子系统的仿真。系统测试可由独立的测试团队执行，并且与系统的规格相关。
**系统集成测试 侧重于测试被测系统以及其他系统和外部服务的接口。系统集成测试需要合适的测试环境，最好与作环境相似。**
验收测试 侧重于确认和证明部署就绪性，这意味着系统满足用户的业务需求。理想情况下，验收测试应由目标用户执行。验收测试的主要形式有：用户验收测试 （UAT）、操作验收测试、合同验收测试和监管验收测试、Alpha 测试和 Beta 测试。

21

---

<!-- Slide 22 -->

2.2.1. 	测试级别 (cont.)
测试级别由以下非详尽的属性列表进行区分，以避免测试活动重叠：
测试对象
测试目标
测试基础
缺陷和故障
方法和责任
22

---

<!-- Slide 23 -->

Question #13
Which types of failures (1-4) fit which test levels (A-D) BEST?
1. Failures in system behavior as it deviates from the user’s business needs
2. Failures in communication between components
3. Failures in logic in a module
4. Failures in not correctly implemented business rules
A. Component testing
B. Component integration testing
C. System testing
D. Acceptance testing
a) 1D, 2B, 3A, 4C
b) 1D, 2B, 3C, 4A
c) 1B, 2A, 3D, 4C
d) 1C, 2B, 3A, 4D

23

---

<!-- Slide 24 -->

2.2.2. 	测试类型
**功能测试 评估组件或系统应执行的功能。这些函数是测试对象应该做的 “什么”。功能测试的主要目标是检查功能完整性、功能正确性和功能适当性。**
**非功能测试 评估组件或系统的功能特征以外的属性。非功能测试是对 “系统行为” 的测试。非功能性测试的主要目标是检查非功能性质量特征。ISO/IEC 25010 标准提供了以下非功能性质量特征的分类：**
性能效率、兼容性、可用性（也称为交互能力）、可靠性、安全 、可维护性、便携性（也称为灵活性） 、安全
有时，在 SDLC 的早期开始非功能性测试是合适的（例如，作为审查或组件测试的一部分）。许多非功能测试是从功能测试派生而来的，因为它们使用相同的功能测试，但要检查在执行功能时是否满足非功能约束（例如，检查功能是否在指定时间内执行，或者功能是否可以移植到新平台）。较晚发现非功能性缺陷可能会对项目的成功构成严重威胁。非功能测试有时需要一个非常具体的测试环境，例如用于可用性测试的可用性实验室。
**黑盒测试 （参见 第 4.2 节）是基于规范的，它从与测试对象的内部结构无关的文档派生测试。黑盒测试的主要目标是根据其规范检查系统的行为。**
**白盒测试 （参见第 4.3 节）是基于结构的，从系统的实现或内部结构（例如，代码、架构、工作流和数据流）派生测试。白盒测试的主要目标是将测试的底层结构覆盖到可接受的级别。**
上述所有四种测试类型都可以应用于所有测试级别，尽管每个级别的重点都不同。可以使用不同的测试技术来推导出所有提到的测试类型的测试条件和测试用例。

24

---

<!-- Slide 25 -->

Question #A9
You work as a tester in a project on a mobile application for food ordering for one of your clients. The client sent you a list of requirements. One of them, with high priority, says
“The order must be processed in less than 10 seconds in 95% of the cases”.
You created a set of test cases in which a number of random orders were made, the processing time measured, and the test results were checked against the requirements.
What test type did you perform?
a) Functional, because the test cases cover the user’s business requirement for the system
b) Non-functional, because the measure the system’s performance
c) Functional, because the test cases interact with the user interface
d) Structural, because we need to know the internal structure of the program to measure the order processing time


25

---

<!-- Slide 26 -->

2.2.3. 	确认测试和回归测试
通常对组件或系统进行更改，以通过添加新功能来增强它，或者通过删除缺陷来修复它。然后，测试还应包括确认测试和回归测试。
**确认测试 确认已成功修复原始缺陷。取决于风险, 可以通过多种方式测试软件的固定版本，包括：**
执行之前由于缺陷而失败的所有测试，或
添加新测试以涵盖修复缺陷所需的任何更改
但是，当修复缺陷时时间或金钱不足时，确认测试可能仅限于简单地执行测试步骤，这些步骤应重现由缺陷引起的故障，并检查故障是否未发生。
26

---

<!-- Slide 27 -->

2.2.3. 	确认测试和回归测试 (cont.)
回归测试 确认更改没有造成不良后果，包括已经过确认测试的修复。这些不利后果可能会影响进行更改的同一组件、同一系统中的其他组件，甚至其他连接的系统。回归测试可能不限于测试对象本身，也可能与环境相关。建议首先执行影响分析以识别回归测试的范围。影响分析显示软件的哪些部分可能会受到影响。
回归测试套件运行多次，通常回归测试用例的数量会随着每次迭代或发布而增加，因此回归测试是自动化的有力候选者。测试自动化应在项目的早期开始。在使用 CI 的情况下，例如在 DevOps 中（请参阅第 2.1.4 节），最好还包括自动回归测试。根据具体情况，这可能包括不同测试级别的回归测试。
如果缺陷已修复和/或对这些测试级别进行了更改，则需要在所有测试级别对测试对象进行确认测试和/或回归测试。

27

---

<!-- Slide 28 -->

Question #14
You are testing a user story with three acceptance criteria: AC1, AC2 and AC3. AC1 is covered by test case TC1, AC2 by TC2, and AC3 by TC3. The test execution history had three test runs on three consecutive versions of the software as follows:
Tests are repeated once you are informed that all defects found in the test run are corrected and a new version of the software is available.
Which of the above tests are executed as regression tests?
a) Only 4, 7, 8, 9
b) Only 5, 7
c) Only 4, 6, 8, 9
d) Only 5, 6


28
#### TC2 passed in Execution 1 (i.e., test (2)), so test (5) is a regression test.
#### Because TC1 and TC3 failed in Execution 1 (i.e., test (1) and test (3)), test (4) and test (6) are confirmation tests.


#### Because TC2 and TC3 failed in Execution 2 (i.e., tests (5) and (6)), test (8) and test (9) are also confirmation tests.
#### TC1 passed in the Execution 2 (i.e., test (4)), so test (7) is also a regression test.

---

<!-- Slide 29 -->

2.3. 维护测试
维护分为不同类别，可以是纠正性的、适应环境变化的或提高性能或可维护性的（有关详细信息，请参阅 ISO/IEC 14764），因此维护可能涉及计划内版本/部署和计划外版本/部署（热修复）。影响分析可以在进行更改之前进行，以帮助根据系统其他区域的潜在后果来决定是否应该进行更改。测试对运行系统的更改包括评估更改实施的成功，以及检查系统中保持不变的部分（通常是系统的大部分）中可能的回归。
维护测试的范围通常取决于：
更改的风险程度
现有系统的大小
更改的大小
29

---

<!-- Slide 30 -->

2.3. 维护测试 (cont.)
维护和维护测试的触发器可分为以下几类：
修改，例如计划的增强（即基于版本）、纠正性更改或热修复。
作环境的升级或迁移，例如从一个平台到另一个平台，这可能需要与新环境以及更改的软件相关联的测试，或者在将数据从另一个应用程序迁移到正在维护的系统时进行数据转换测试。
停用，例如当应用程序达到其生命周期结束时。当系统停用时，如果需要较长的数据保留期，则可能需要测试数据存档。如果在存档期间需要某些数据，则可能还需要在存档后测试还原和检索过程。

30

---

<!-- Slide 31 -->

Question #A10
Your organization’s test strategy suggests that once a system is going to be retired, data migration shall be tested. As part of what test type is this testing MOST likely to be performed?
a) Maintenance testing
b) Regression testing
c) Component testing
d) Integration testing

31

---

<!-- Slide 32 -->

3. 静态测试 – 80 分钟


---

<!-- Slide 33 -->

关键字
异常， 动态测试，
正式审查， 非正式审查，
检查， 审查，
静态分析， 静态测试，
技术审查， 演练
33

---

<!-- Slide 34 -->

第 3 章的学习目标：
3.1 静态测试基础
FL-3.1.1 	（K1）识别可以通过静态测试检查的工作产品类型
FL-3.1.2 	（K2）解释静态测试的价值
FL-3.1.3 	（K2）比较和对比静态测试和动态测试
3.2 反馈和审核流程
FL-3.2.1 （K1）确定早期和频繁的利益相关方反馈的好处
FL-3.2.2 （K2）总结审查流程的活动
FL-3.2.3 （K1）回顾在执行审查时分配给主体角色的职责
FL-3.2.4 （K2）比较和对比不同的评论类型
FL-3.2.5 （K1）回顾导致审查成功的因素

34

---

<!-- Slide 35 -->

3.1. 静态测试基础
与动态测试相反，在静态测试中，不需要执行被测软件。
代码、流程规范、系统架构规范或其他工作产品通过人工检查（例如审查）或借助工具（例如静态分析）进行评估。
测试目标包括提高质量、检测缺陷和评估可读性、完整性、正确性、可测试性和一致性等特征。静态测试可用于验证和确认。
测试人员、业务代表（产品负责人、业务分析师等）和开发人员在示例映射、协作用户故事编写和 backlog 细化会议期间一起工作，以确保用户故事和相关工作产品满足定义的标准，例如，就绪的定义（参见第 5.1.3 节）。
可以应用审查技术来确保用户情景完整且易于理解，并包括可测试的验收标准。通过提出正确的问题，测试人员可以探索、挑战并帮助改进提议的用户故事。
35

---

<!-- Slide 36 -->

3.1. 静态测试基础 (cont.)
静态分析可以在动态测试之前发现问题，同时通常需要更少的工作量，因为不需要测试用例，并且通常使用工具（参见第 6 章）。
静态分析通常被纳入 CI 框架中（参见第 2.1.4 节）。
虽然静态分析主要用于检测特定的代码缺陷，但也用于评估可维护性和安全性。
拼写检查器和可读性工具是静态分析工具的其他示例。

36

---

<!-- Slide 37 -->

3.1.1. 	可通过静态测试检查的工作产品
几乎所有工作产品都可以使用静态测试进行检查。示例包括需求规范文档、源代码、测试计划、测试用例、产品积压工作项、测试章程、项目文档、合同和模型。
任何可以阅读和理解的工作成果都可以成为评审的主题。然而，对于静态分析，工作产品需要一个可以检查的结构（例如，具有正式语法的模型、代码或文本）。
不适合静态测试的工作产品包括那些难以被人类解释且不应使用工具分析的工作产品（例如，由于法律原因，第三方可执行代码）。
37

---

<!-- Slide 38 -->

Question #A11
The following is a list of the work products produced in the SDLC.
i) Business requirements
ii) Schedule
iii) Test budget
iv) Third-party executable code
v) User stories and their acceptance criteria
Which of them can be reviewed?
a) i and iv can be reviewed
b) i, ii, iii and iv can be reviewed
c) i, ii, iii, and v can be reviewed
d) iii, iv, v can be reviewed

38

---

<!-- Slide 39 -->

3.1.2. 	静态测试的价值
静态测试可以在 SDLC 的最早阶段检测到缺陷，满足早期测试的原则（参见第 1.3 节）。它还可以识别动态测试无法检测到的缺陷（例如，无法访问的代码、未按预期实现的设计模式、不可执行的工作产品中的缺陷）。
静态测试提供了评估工作产品的质量并建立对工作产品的信心的能力。通过验证记录的需求，利益相关者还可以确保这些需求描述了他们的实际需求。由于静态测试可以在 SDLC 的早期执行，因此可以在相关利益相关者之间建立共识。相关利益相关者之间的沟通也将得到改善。因此，建议让各种利益相关者参与静态测试。
尽管实施审核的成本可能很高，但总体项目成本通常比不执行审核时低得多，因为在项目后期修复缺陷所需的时间和精力更少。
与动态测试相比，使用静态分析可以更有效地检测某些代码缺陷，这通常可以减少代码缺陷并降低总体开发工作量。
39

---

<!-- Slide 40 -->

Question #A12
Decide which of the following statements (i-v) are true for static testing.
i) Abnormal external behaviors are easier to identify with this testing
ii) Discrepancies from a coding standard are easier to find with this testing
iii) It identifies failures caused by defects when the software is run
iv) Its test objective is to identify defects as early as possible
v) Missing coverage for critical security requirements is easier to find and fix
a) i, iv, v are true for static testing
b) i, iii, iv are true for static testing
c) ii, iii are true for static testing
d) ii, iv, v are true for static testing


40

---

<!-- Slide 41 -->

3.1.3. 	静态测试和动态测试之间的区别
静态测试和动态测试实践相辅相成。它们具有相似的目标，例如支持检测工作产品中的缺陷（参见第 1.1.1 节），但也存在一些差异，例如：
静态测试和动态测试（包括故障分析）都可以检测到缺陷，但是有些缺陷类型只能通过静态或动态测试来发现。
静态测试直接发现缺陷，而动态测试导致failures，通过后续分析确定相关缺陷
静态测试可以更容易地检测出代码路径上的缺陷，这些缺陷很少执行或使用动态测试难以到达
静态测试可以应用于不可执行的工作产品，而动态测试只能应用于可执行的工作产品
静态测试可用于测量不依赖于执行代码的质量特征（例如，可维护性），而动态测试可用于测量依赖于执行代码的质量特征（例如，性能效率）

41

---

<!-- Slide 42 -->

3.1.3. 	静态测试和动态测试之间的区别 (cont.)
通过静态测试更容易和/或更便宜地发现的典型缺陷包括：
需求缺陷（例如，不一致、歧义、矛盾、遗漏、不准确、重复）
设计缺陷（例如，数据库结构效率低下、模块化程度差）
某些类型的编码缺陷（例如，具有未定义值的变量、未声明的变量、无法访问或重复的代码、代码复杂性过高）
偏离标准（例如，不遵守编码标准中的命名约定）
接口规范不正确（例如，参数的数量、类型或顺序不匹配）
特定类型的安全漏洞（例如缓冲区溢出）
测试基础覆盖率的差距或不准确（例如，缺少验收标准的测试）
42

---

<!-- Slide 43 -->

Question #15
Which of the following is NOT a benefit of static testing?
a) Having less expensive defect management due to the ease of detecting defects later in the SDLC
b) Fixing defects found during static testing is generally much less expensive than fixing defects found during dynamic testing
c) Finding coding defects that might not have been found by only performing dynamic testing
d) Detecting gaps and inconsistencies in requirements

43

---

<!-- Slide 44 -->

3.2. 反馈和Review (审查)流程 3.2.1. 尽早和频繁地提供利益相关者反馈的好处
尽早和频繁的反馈有助于尽早沟通潜在的质量问题。
如果在 SDLC 期间几乎没有利益相关者的参与，则正在开发的产品可能无法满足利益相关者的原始或当前愿景。
未能交付利益相关者想要的东西可能会导致代价高昂的返工、错过最后期限、推卸责任，甚至可能导致项目完全失败。
在整个 SDLC 中，利益相关者的频繁反馈可以防止对需求的误解，并确保更早地理解和实施对需求的更改。
这有助于开发团队提高他们对正在构建的内容的理解。
它使他们能够专注于那些为利益相关者提供最大价值并对已识别风险产生最积极影响的功能。
44

---

<!-- Slide 45 -->

Question #16
Which of the following is a benefit of early and frequent feedback?
a) It improves the test process for future projects
b) It forces customers to prioritize their requirements based on agreed risks
c) It  provides a measure for the quality of changes
d) It helps avoid requirements misunderstandings

45

---

<!-- Slide 46 -->

3.2.2. 	Review 流程活动
ISO/IEC 20246 标准定义了一个通用的审查流程，该流程提供了一个结构化但灵活的框架，可以根据该框架针对特定情况定制特定的审查流程。如果所需的审查更正式，则需要为不同活动描述的更多任务。
许多工作成果的规模使它们太大，无法被单个评论涵盖。可以多次调用审查流程以完成整个工作产品审查。
46

---

<!-- Slide 47 -->

3.2.2. 	Review 流程活动 (cont.)
**规划。 在规划阶段，应定义审查的范围，包括目的、要审查的工作成果、要评估的质量特征、要关注的领域、退出标准、支持信息（如标准）、工作和审查的时间框架。**
**审查开始。 在审查启动期间，目标是确保所有相关人员都已准备好开始审查。这包括确保每个参与者都可以访问正在审查的工作产品，了解他们的角色和职责，并获得执行审查所需的一切。**
个人评论。 每个审查者执行单独的审查，以评估被审查工作产品的质量，并通过应用一种或多种审查技术（例如，基于清单的审查、基于情景的审查）来识别异常、建议和问题。ISO/IEC 20246 标准对不同的审查技术提供了更深入的了解。审阅者记录他们发现的所有异常、建议和问题。
沟通和分析。 由于在审查过程中发现的异常不一定是缺陷，因此所有这些异常都需要分析和讨论。对于每个异常，应根据其状态、所有权和所需作做出决定。这通常在审查会议上完成，在此期间，参与者还决定被审查的工作产品的质量水平以及需要采取哪些后续行动。可能需要后续审查才能完成作。
**修复和报告。 对于每个缺陷，都应创建缺陷报告，以便可以采取纠正措施。一旦达到退出标准，就可以接受工作成果。报告审查结果。**

47

---

<!-- Slide 48 -->

3.2.3. 	 Reviews中的角色和职责
**经理 – 决定要审查的内容并提供资源，例如员工和审查时间**
**作者 – 创建并修复正在审查的工作产品**
**主持人Moderator （也称为facilitator引导员 ）– 确保审查会议的有效运行，包括调解、时间管理和每个人都可以自由发言的安全审查环境**
**抄写员Scribe（也称为记录员recorder ）— 整理来自审查者的异常并记录审查信息，例如在审查会议期间发现的决定和新异常**
**审查员 – 执行审查。审查者可以是参与项目的人员、主题专家或任何其他利益干系人**
**审查负责人 – 全面负责审查，例如决定谁将参与，以及组织审查的时间和地点**
其他更详细的角色是可能的，如 ISO/IEC 20246 标准中所述。
48

---

<!-- Slide 49 -->

3.2.4. 	Review类型
存在许多审查类型，从非正式审查到正式审查。所需的正式程度取决于各种因素，例如所遵循的 SDLC、开发过程的成熟度、被审查工作成果的关键性和复杂性、法律或法规要求以及对审计跟踪的需求。相同的工作成果可以用不同的审查类型进行审查，例如，首先是非正式的，然后是更正式的。
选择正确的审查类型是实现所需审查目标的关键（请参阅第 3.2.5 节）。选择不仅基于目标，还基于项目需求、可用资源、工作产品类型和风险、业务领域和公司文化等因素。
49

---

<!-- Slide 50 -->

3.2.4. 	Review类型 (cont.)
**非正式审查。 非正式审查不遵循既定的流程，也不需要正式的书面结果。主要目标是检测异常。**
演练 (Walkthrough)。 由作者领导的演练可以实现许多目标，例如评估质量和建立对工作产品的信心、教育审查者、获得共识、产生新想法、激励和使作者能够改进和检测异常。审查者可能会在演练之前执行单个审查，但这不是必需的。
**技术审查。 技术审查由技术合格的审查人员执行，并由主持人领导。技术审查的目标是获得共识并就技术问题做出决策，但也要检测异常情况、评估质量并建立对工作产品的信心、产生新想法，以及激励和使作者能够改进。**
检查 (Inspection)。 由于检查是最正式的审查类型，因此它们遵循完整的通用流程（参见第 3.2.2 节）。主要目标是查找最大数量的异常。其他目标是评估质量，建立对工作成果的信心，以及激励和使作者能够改进。收集指标并用于改进 SDLC，包括检查流程。在检查中，作者不能充当审查负责人或抄写员。

50

---

<!-- Slide 51 -->

Question #17
The reviews being used in your organization have the following attributes:
There is the role of a scribe
The main purpose is to evaluate quality
The meeting is led by the author of the work product
There is individual preparation
A review report is produced
Which of the following review types is MOST likely being used?
a) Informal review
b) Walkthrough
c) Technical review
d) Inspection

51

---

<!-- Slide 52 -->

3.2.5. 	Review的成功因素
定义明确的目标和可衡量的退出标准。对参与者的评估永远不应该是一个目标
选择合适的评审类型以实现给定的目标，并适合工作产品的类型、评审参与者、项目需求和背景
对小块进行审核，以便审核员在个人审核和/或审核会议（举行时）期间不会注意力不集中
向利益相关者和作者提供评论的反馈，以便他们能够改进产品及其活动（请参阅第 3.2.1 节）
为参与者提供足够的时间来准备审查
管理层对审核过程的支持
使审核成为组织文化的一部分，以促进学习和流程改进
为所有参与者提供足够的培训，以便他们知道如何履行自己的职责
为会议提供便利
52

---

<!-- Slide 53 -->

Question #18
Which of these statements is NOT a factor that contributes to successful reviews?
a) Participants should dedicate adequate time for the review
b) Splitting large work products into small parts to make the required effort less intense
c) Participants should avoid behaviors that might indicate boredom, exasperation, or hostility to other participants
d) Failures found should be acknowledged, appreciated, and handled objectively


53

---
