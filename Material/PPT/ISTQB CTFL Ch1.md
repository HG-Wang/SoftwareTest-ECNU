<!-- Slide 1 -->

1. 测试基础 – 180 分钟


---

<!-- Slide 2 -->

关键字
覆盖率， 调试， 缺陷， 错误， 失败，
质量， 质量保证， 根本原因，
测试分析， 测试基础， 测试用例， 测试完成， 测试条件， 测试控制， 测试数据，
测试设计， 测试执行， 测试实施， 测试监控， 测试对象，
测试目标， 测试计划， 测试程序， 测试过程， 测试结果，
测试， 测试件， 可追溯性， 验证， 验证
2

---

<!-- Slide 3 -->

第 1 章学习目标
1.1 什么是测试？
FL-1.1.1 	（K1）确定典型测试目标
FL-1.1.2 	（K2）区分测试与调试
1.2 为什么需要测试？
FL-1.2.1 	（K2）举例说明为什么需要测试
FL-1.2.2 	（K1）回顾测试与质量保证之间的关系
FL-1.2.3 	（K2）区分根本原因、错误、缺陷和故障
1.3 测试原则
FL-1.3.1 	（K2）解释七项测试原则

3

---

<!-- Slide 4 -->

第 1 章学习目标(cont.)
1.4 测试活动、测试件和测试角色
FL-1.4.1 （K2）解释不同的测试活动和相关任务
FL-1.4.2 （K2）解释上下文对测试过程的影响
FL-1.4.3 （K2）区分支持测试活动的测试软件
FL-1.4.4 （K2）解释维护可追溯性的价值
FL-1.4.5 （K2）比较测试中的不同角色
1.5 测试的基本技能和良好实践
FL-1.5.1 	（K2）举例说明测试所需的通用技能
FL-1.5.2 	（K1）回顾整个团队方法的优势
FL-1.5.3 	（K2）区分独立测试的优缺点

4

---

<!-- Slide 5 -->

1.1. 什么是测试？
**软件测试评估软件质量，并有助于降低软件运行失败的风险。**
**软件测试是一组用于发现缺陷和评估软件工作产品质量的活动。**
**这些工作产品在进行测试时称为测试对象。**
关于测试的常见误解
测试只包括执行测试（即运行软件和检查测试结果）。但是，软件测试还包括其他活动，并且必须与软件开发生命周期保持一致（参见第 2 章）。
**测试完全集中在验证测试对象上。虽然测试涉及验证，即检查系统是否满足特定要求，但也涉及确认，这意味着检查系统是否满足用户和其他利益相关者在其作环境中的需求。**
ISO/IEC/IEEE 29119-1 标准提供了有关软件测试概念的更多信息。
5

---

<!-- Slide 6 -->

1.1. 什么是测试？ (cont.)
测试可以是动态的或静态的。
**动态测试涉及软件的执行，而静态测试则不涉及。**
**静态测试包括评论（参见第 3 章）和静态分析。**
动态测试使用不同类型的测试技术和测试方法来派生测试用例（参见第 4 章）。
测试不仅仅是一项技术活动。它还需要得到适当的规划、管理、估计、监测和控制（见第 5 章）。
测试人员使用工具（见第 6 章），但重要的是要记住，测试在很大程度上是一项智力活动，要求测试人员具备专业知识，使用分析技能并应用批判性思维和系统思维（Myers 2011，Roman 2018）。
6

---

<!-- Slide 7 -->

1.1.1. 	测试目标
典型的测试目标是：
评估工作产品，例如需求、用户情景、设计和代码
导致故障和发现缺陷
确保测试对象所需的覆盖率
降低软件质量不足的风险级别
验证是否满足了指定的要求
验证测试对象是否符合合同、法律和法规要求
向利益相关者提供信息，使他们能够做出明智的决策
建立对测试对象质量的信心
验证测试对象是否完整并按利益相关者的预期工作
测试目标可能会有所不同，具体取决于环境，包括正在测试的工作产品、测试级别、风险、所遵循的软件开发生命周期 （SDLC） 以及与业务环境相关的因素，例如，公司结构、竞争考虑因素或上市时间。
7

---

<!-- Slide 8 -->

Question #1
Which of the following statements describe a valid test objective?
a) To prove that there are no unfixed defects in the system under test
b) To prove that there will be no failures after the implementation of the system into production
c) To reduce the risk level of the test object and to build confidence in the quality level
d) To verify that there are no untested combinations of inputs

8

---

<!-- Slide 9 -->

1.1.2. 	测试和调试
测试和调试是单独的活动。
测试可以触发由软件缺陷引起的failures（动态测试），也可以直接发现测试对象中的defects （静态测试）。
当动态测试（参见第 4 章）触发failure时，调试涉及查找此故障的原因（defects），分析这些原因并消除它们。在这种情况下，典型的调试过程包括：
故障重现
诊断（发现缺陷）
修复缺陷
**后续的确认测试将检查修复是否解决了问题。确认测试最好由执行初始测试的同一人完成。**
**还可以执行后续的回归测试，以检查修复是否导致测试对象的其他部分失败（有关确认测试和回归测试的更多信息，请参见 Section 2.2.3）。**
当静态测试识别出缺陷时，调试与删除它有关。无需复制或诊断，因为静态测试直接发现缺陷，并且不会导致failures （参见第 3 章）。
9

---

<!-- Slide 10 -->

Question #A1
You were given a task to analyze and fix causes of failures in a new system to be released.
Which activity are you performing?
a) Debugging
b) Software testing
c) Requirement elicitation
d) Defect management

10

---

<!-- Slide 11 -->

1.2. 为什么需要测试？
测试作为质量控制的一种形式，有助于在设定的范围、时间、质量和预算限制内实现商定的测试目标。
测试对成功的贡献不应局限于测试团队活动。任何利益相关者都可以利用他们的测试技能使项目更接近成功。
测试组件、系统和相关的工作产品（例如，文档）有助于识别软件中的缺陷。
11

---

<!-- Slide 12 -->

1.2.1. 	测试对成功的贡献
**测试提供了一种经济高效的缺陷检测方法。然后可以删除这些缺陷（通过调试 - 非测试活动），因此测试间接有助于更高质量的测试对象。**
**测试提供了一种在 SDLC 的各个阶段直接评估测试对象质量的方法。这些措施被用作大型项目管理活动的一部分，有助于决策进入 SDLC 的下一阶段，例如发布决策。**
**测试为用户提供了开发项目的间接表示。测试人员确保在整个开发生命周期中考虑他们对用户需求的理解。另一种选择是将一组有代表性的用户作为开发项目的一部分，由于成本高且缺乏合适的用户，这通常是不可能的。**
可能还需要进行测试以满足合同或法律要求，或符合监管标准。
12

---

<!-- Slide 13 -->

Question #2
Which of the following options shows an example of test activities that contribute to success?
a) Having testers involved during various software development lifecycle (SDLC) activities will help to detect defects in work products
b) Testers try not to disturb the developers while coding, so that the developers write better code
c) Testers collaborating with end users help to improve the quality of defect reports during component integration and system testing
d) Certified testers will design much better test cases than non-certified testers

13

---

<!-- Slide 14 -->

1.2.2. 	测试和质量保证 （QA）
**测试是一种以产品为导向的纠正方法，侧重于支持达到适当质量水平的活动。测试是质量控制的一种主要形式，而其他形式包括形式化方法（模型检查和正确性证明）、模拟和原型设计。**
**QA 是一种以流程为导向的预防性方法，侧重于流程的实施和改进。它的工作原理是，如果正确遵循一个好的流程，那么它将产生一个好的产品。QA 适用于开发和测试过程，并且是项目中每个人的责任。**
测试结果由 QA 和测试使用。
在测试中，它们用于修复缺陷，
在 QA 中，它们提供有关开发和测试过程执行情况的反馈。
14

---

<!-- Slide 15 -->

Question #A2
In many software organizations the test department is called the Quality Assurance (QA) department. Is this sentence correct or not and why?
a) It is correct. Testing and QA mean exactly the same thing
b) It is correct. These names can be used interchangeably because both testing and QA focus their activities on the same quality issues
c) It is not correct. Testing is something more; testing includes all activities with regard to quality. QA focuses on quality-related processes
d) It is not correct. QA is focused on quality-related processes while testing concentrates on demonstrating that a component or system is fit for purpose and to detect defects

15

---

<!-- Slide 16 -->

1.2.3. Errors, Defects, Failures, and Root Causes
人犯errors（Mistakes），这会产生defects（faults、bugs），这反过来又可能导致failures 。
人类犯错的原因有很多，例如时间压力、工作产品、流程、基础设施或交互的复杂性，或者仅仅是因为他们疲倦或缺乏足够的培训。
Defects可以在文档（例如需求规范或测试脚本）、源代码或支持工作产品（例如构建文件）中找到。
在 SDLC 中早期产生的工作产品中的缺陷如果未被发现，通常会导致生命周期后期的工作产品有缺陷。
如果执行代码中的缺陷，系统可能无法执行它应该执行的作，或者执行它不应该执行的作，从而导致失败。
有些缺陷在执行时总是会导致失败，而另一些缺陷只会在特定情况下导致失败，而有些缺陷可能永远不会导致失败。
16

---

<!-- Slide 17 -->

1.2.3. Errors, Defects, Failures, and Root Causes (cont.)
errors和defects并不是导致failures的唯一原因。failures也可能由环境条件引起，例如当辐射或电磁场导致固件缺陷时。
根本原因是问题发生的根本原因（例如，导致错误的情况）。通过根本原因分析来确定根本原因，通常在发生故障或发现缺陷时进行。人们相信，通过解决根本原因（例如消除它），可以防止更多类似的failures或defects或降低其频率。

17

---

<!-- Slide 18 -->

Question #A3
A phone ringing in a neighboring cubicle distracts a programmer causing him to improperly program the logic that checks the upper boundary of an input variable. Later, during system testing, a tester notices that this input field accepts invalid input values.
Which of the following correctly describes an incorrectly coded upper bound?
a) The root cause
b) A failure
c) An error
d) A defect


18

---

<!-- Slide 19 -->

1.3. 测试原则
**测试显示的是缺陷的存在，而不是不存在缺陷。**
测试可以显示测试对象中存在缺陷，但不能证明没有缺陷 （Buxton 1970）。
测试可以降低测试对象中未发现缺陷的可能性，但即使未发现缺陷，测试也无法证明测试对象的正确性。
**穷尽的测试是不可能的。**
除了微不足道的情况外，测试所有事情都是不可行的（Manna 1978）。
与其试图穷尽地测试，不如使用测试技术（参见第 4 章）、测试用例优先级（参见第 5.1.5 节）和基于风险的测试（参见第 5.2 节）来集中测试工作。
19

---

<!-- Slide 20 -->

1.3. 测试原则 (cont.)
**早期测试可节省时间和金钱。**
在流程早期消除的缺陷不会导致衍生工作产品中出现后续缺陷。质量成本将降低，因为 SDLC 后期发生的故障会更少 （Boehm 1981）。
为了及早发现缺陷，静态测试（参见第 3 章）和动态测试（参见第 4 章）都应该尽早开始。
**缺陷聚集在一起。**
少量的系统组件通常包含大部分已发现的缺陷或导致大多数作故障 （Enders 1975）。这种现象是帕累托原则的一个例子。
预测的缺陷簇，以及在测试或运行期间观察到的实际缺陷簇，是基于风险的测试的重要输入（参见第 5.2 节）。

20

---

<!-- Slide 21 -->

1.3. 测试原则 (cont.)
**测试会磨损。**
如果相同的测试重复多次，它们在检测新缺陷方面会变得越来越无效 （Beizer 1990）。
为了克服这种影响，可能需要修改现有测试和测试数据，并且可能需要编写新的测试。
然而，在某些情况下，重复相同的测试可能会产生有益的结果，例如，在自动回归测试中（参见 2.2.3 节）。
**测试取决于上下文。**
没有单一的普遍适用的测试方法。在不同的环境中进行测试的方式不同 （Kaner 2011）。
**“缺陷不存在”的谬误。**
期望软件验证将确保系统的成功是一种谬论（即误解）。
彻底测试所有指定要求并修复发现的所有缺陷可能仍然会产生一个不能满足用户需求和期望的系统，无助于实现客户的业务目标，并且与其他竞争系统相比更差。
除了verification之外，还应进行validation （Boehm 1981）。
21

---

<!-- Slide 22 -->

Question #3
You have been assigned as a tester to a team producing a new system incrementally. You have noticed that no changes have been made to the existing regression test cases for several iterations and no new regression defects were identified. Your manager is happy, but you are not. Which testing principle explains your skepticism?
a) Tests wear out
b) Absence-of-errors fallacy
c) Defects cluster together
d) Exhaustive testing is impossible


22

---

<!-- Slide 23 -->

1.4. 测试活动、测试件和测试角色
测试与上下文相关，但在高级别上，存在一组常见的测试活动，没有这些活动，测试就不太可能实现测试目标。这些测试活动集构成一个测试流程。测试过程可以根据各种因素针对给定情况进行定制。此测试过程包括哪些测试活动，如何实现它们以及何时发生，通常是作为针对特定情况的测试计划的一部分来决定的（参见 5.1 节）。
以下各节从测试活动和任务、上下文的影响、测试件、测试基础和测试软件之间的可追溯性以及测试角色方面描述了此测试过程的一般方面。
ISO/IEC/IEEE 29119-2 标准提供了有关测试过程的更多信息。
23

---

<!-- Slide 24 -->

1.4.1. 	测试活动和任务
**测试计划**
包括定义测试目标，然后在整体上下文施加的约束范围内选择最能实现目标的方法。
测试计划将在 5.1 节中进一步解释。
**测试监控和测试控制。**
测试监控包括对所有测试活动的持续检查，以及将实际进度与计划进行比较。
测试控制涉及采取必要的措施来满足测试目标。
测试监控和测试控制将在 5.3 节中进一步解释。
24

---

<!-- Slide 25 -->

1.4.1. 	测试活动和任务 (cont.)
**测试分析**
包括分析测试基础以识别可测试的特征。定义相关的测试条件并确定其优先级，同时考虑相关风险和风险级别（参见第 5.2 节）。
还评估测试基础和测试对象，以识别它们可能包含的缺陷并评估其可测试性。
测试分析通常通过使用测试技术来支持（参见第 4 章）。
测试分析根据可衡量的覆盖率标准回答了 “测试什么 ”的问题。
**测试设计**
包括将测试条件详细阐述为测试用例和其他测试件（例如，测试章程test charters）。此活动通常涉及 coverage 项的标识，这些项用作指定测试用例输入的指南。
测试技术（4） 可用于支持此活动。
测试设计还包括定义测试数据要求、设计测试环境以及确定必要的基础设施和工具。
测试设计回答了 “how to test？” 这个问题。
25

---

<!-- Slide 26 -->

1.4.1. 	测试活动和任务 (cont.)
**测试实现**
包括创建或获取测试执行所需的测试件（例如，测试数据）。测试用例可以组织到测试过程中，这些测试过程通常组装成测试套件。创建手动和自动测试脚本。
测试程序在测试执行计划中进行优先级排序和安排，以实现高效的测试执行（参见 5.1.5 节）。测试环境已构建并验证已正确设置。
**测试执行**
包括根据测试执行计划运行测试（测试运行）。测试执行可以是手动的，也可以是自动的。
测试执行可以采取多种形式，包括持续测试或结对测试会话。将实际测试结果与预期结果进行比较。记录测试结果。分析异常以确定其可能的原因。
此分析允许我们根据观察到的故障报告异常（请参阅第 5.5 节）。
26

---

<!-- Slide 27 -->

1.4.1. 	测试活动和任务 (cont.)
**测试完成**
通常发生在项目里程碑（例如，发布、迭代结束、测试级别完成）时。
对于任何未解决的缺陷，将创建更改请求或产品积压工作项。
任何将来可能有用的测试软件都会被识别并存档或移交给适当的团队。
测试环境将关闭到商定的状态。
对测试活动进行分析，以确定经验教训和对未来迭代、发布或项目的改进（参见 2.1.6 节）。
创建测试完成报告并将其传达给利益相关者。

27

---

<!-- Slide 28 -->

Question #4
You work in a team that develops a mobile application for food ordering. In the current iteration the team decided to implement the payment functionality.
Which of the following activities is a part of test analysis?
a) Estimating that testing the integration with the payment service will take 8 person-days
b) Deciding that the team should test if it is possible to properly share payment between many users
c) Using boundary value analysis (BVA) to derive the test data for the test cases that check the correct payment processing for the minimum allowed amount to be paid
d) Analyzing the discrepancy between the actual result and expected result after executing a test case that checks the process of payment with a credit card, and reporting a defect

28

---

<!-- Slide 29 -->

Question #A4
Consider the following testware.





Which test activity produces this testware as an output?
a) Test planning
b) Test monitoring and control
c) Test analysis
d) Test design

29

---

<!-- Slide 30 -->

1.4.2. 	在上下文中测试流程
测试不是孤立进行的。测试活动是组织内部执行的开发流程不可或缺的一部分。测试也由利益相关者资助，其最终目标是帮助满足利益相关者的业务需求。因此，进行测试的方式将取决于许多背景因素，包括：
利益相关者（需求、期望、要求、合作意愿等）
团队成员（技能、知识、经验水平、可用性、培训需求等）
业务领域（测试对象的关键性、已识别的风险、市场需求、特定法律法规等）
技术因素（软件类型、产品架构、使用的技术等）
项目约束（范围、时间、预算、资源等）
组织因素（组织结构、现有政策、使用的做法等）
软件开发生命周期（工程实践、开发方法等）
工具（可用性、可用性、合规性等）
这些因素将对许多与测试相关的问题产生影响，包括：测试策略、使用的测试技术、测试自动化程度、所需的覆盖率、测试软件的详细程度、测试报告等。
30

---

<!-- Slide 31 -->

Question #5
Which of the following factors have a SIGNIFICANT influence on the test approach?
i) The SDLC
ii) The number of defects detected in previous projects
iii) The identified product risks
iv) New regulatory requirements forcing formal white-box testing
v) The test environment setup
a) i, ii have significant influence
b) i, iii, iv have significant influence
c) ii, iv, v have significant influence
d) iii, v have significant influence

31

---

<!-- Slide 32 -->

1.4.3. 	测试件
Testware 是作为 Section 1.4.1 中描述的测试活动的输出工作产品创建的。
不同组织生产、塑造、命名、组织和管理其工作产品的方式存在显着差异。
适当的配置管理（参见 5.4 节）确保工作产品的一致性和完整性。
以下工作产品列表并不详尽：
测试计划工作产品 包括：测试计划、测试计划、风险登记簿、进入标准和退出标准（参见第 5.1 节）。风险登记册是风险列表，包括风险可能性、风险影响和有关风险缓解的信息（参见第 5.2 节）。测试计划、风险登记、进入标准和退出标准通常是测试计划的一部分。
**测试监测和测试控制工作产品 包括：测试进度报告（参见第 5.3.2 节）、控制指令文档（参见第 5.3 节）和有关风险的信息（参见第 5.2 节）。**
**测试分析工作产品 包括：（优先的）测试条件（例如，验收标准，参见第 4.5.2 节）和有关测试基础中缺陷的缺陷报告（如果未直接修复）。**
32

---

<!-- Slide 33 -->

1.4.3. 	测试件 (cont.)
工作产品列表（续）
**测试设计工作产品 包括：（优先的）测试用例、测试章程、覆盖率项、测试数据需求和测试环境需求。**
**测试实施工作产品 包括：测试过程、手动和自动测试脚本、测试套件、测试数据、测试执行计划和测试环境项。测试环境项的示例包括：存根、驱动程序、模拟器和服务虚拟化。**
**测试执行工作产品 包括：测试日志和缺陷报告（请参阅第 5.5 节）。**
**测试完成工作产品 包括：测试完成报告（参见第 5.3.2 节）、改进后续项目或迭代的行动项、记录的经验教训和变更请求（例如，作为产品积压工作项）。**

33

---

<!-- Slide 34 -->

1.4.4. 	Test Basis 和 Testware 之间的可追溯性
**为了实施有效的测试监控和测试控制，在整个测试过程中，在测试基础元素、与这些元素相关的测试件（例如，测试条件、风险、测试用例）、测试结果和缺陷之间建立和维护可追溯性非常重要。**
**准确的可追溯性支持覆盖率评估，因此如果在测试基础中定义了可测量的覆盖率标准，则非常有用。覆盖率标准可以作为关键绩效指标，以推动显示测试目标已实现程度的活动（参见第 1.1.1 节）。例如：**
测试用例对需求的可追溯性可以验证测试用例是否覆盖了需求。
测试结果对风险的可追溯性可用于评估测试对象中的残余风险水平。
除了评估覆盖率之外，良好的可追溯性还可以确定变更的影响，促进审计，并有助于满足 IT 监管标准。良好的可追溯性还通过包含测试基础元素的状态，使测试进度报告和测试完成报告更容易理解。这也有助于以易于理解的方式向利益相关者传达测试的技术方面。可追溯性提供信息，用于根据业务目标评估产品质量、流程能力和项目进度。
34

---

<!-- Slide 35 -->

1.4.5. 	测试中的角色
**在本教学大纲中，涵盖了测试中的两个主要角色：测试管理角色和测试角色。分配给这两个角色的活动和任务取决于项目和产品上下文、角色中人员的技能以及组织等因素。**
**测试管理角色全面负责测试流程、测试团队和测试活动的领导。**
测试管理角色主要集中在测试计划、测试监控、测试控制和测试完成等活动。
执行测试管理角色的方式因上下文而异。例如，在 Agile 软件开发中，一些测试管理任务可能由 Agile 团队处理。跨多个团队或整个组织的任务可能由开发团队之外的测试经理执行。
**测试角色全面负责测试的工程（技术）方面。**
测试角色主要集中在测试分析、测试设计、测试实施和测试执行等活动上。
不同的人可能在不同的时间担任这些角色。例如，测试管理角色可以由团队领导、测试经理、开发经理等执行。一个人也可以同时担任测试和测试管理的角色。
35

---

<!-- Slide 36 -->

Question #6
Which TWO of the following tasks belong MAINLY to a testing role?
a) Configure test environments
b) Maintain the product backlog
c) Design solutions to new requirements
d) Create the test plan
e) Analyze the test basis

36

---

<!-- Slide 37 -->

1.5. 测试的基本技能和良好实践
技能是来自一个人的知识、实践和才能做好某事的能力。
优秀的测试人员应该具备一些基本技能来做好他们的工作。
优秀的测试人员应该是有效的团队合作者，并且应该能够在不同级别的测试独立性上执行测试。
37

---

<!-- Slide 38 -->

1.5.1. 	测试所需的通用技能
虽然是通用的，但以下技能与测试人员特别相关：
测试知识（提高测试的有效性，例如，通过使用测试技术）
彻底、细心、好奇心、注重细节、有条不紊（识别缺陷，尤其是难以发现的缺陷）
良好的沟通技巧，积极倾听，具有团队合作精神（与所有利益相关者有效互动，将信息传达给他人，被理解，以及报告和讨论缺陷）
分析性思维、批判性思维、创造力（提高测试的有效性）
技术知识（提高测试效率，例如，使用适当的测试工具）
领域知识（能够理解最终用户/业务代表并与之沟通）
测试人员通常是坏消息的传播者。责怪坏消息的传播者是人类的普遍特征。这使得沟通技巧对测试人员至关重要。传达测试结果可能会被视为对商品及其作者的批评。确认偏差会使人难以接受与当前持有的信念不同的信息。有些人可能会认为测试是一种破坏性活动，尽管它对项目成功和产品质量有很大帮助。为了尝试改进这种观点，应以建设性的方式传达有关缺陷和故障的信息。
38

---

<!-- Slide 39 -->

Question #7
Which of the following skills (i-v) are the MOST important skills of a tester?
i) Having domain knowledge
ii) Creating a product vision
iii) Being a good team player
iv) Planning and organizing the work of the team
v) Critical thinking
a) ii and iv are important
b) i, iii and v are important
c) i, ii and v are important
d) iii and iv are important

39

---

<!-- Slide 40 -->

1.5.2. 	完整团队方法
**测试人员的重要技能之一是在团队环境中有效工作并为团队目标做出积极贡献的能力。完整团队方法 - 来自极限编程的实践（参见 2.1 节） - 建立在这项技能之上。**
在完整团队方法中，任何具有必要知识和技能的团队成员都可以执行任何任务，每个人都对质量负责。团队成员共享相同的工作区（物理或虚拟），因为同地协作促进了沟通和互动。完整团队方法改善了团队动力，增强了团队内部的沟通和协作，并通过允许利用团队内的各种技能来创造协同效应，从而使项目受益。
测试人员与其他团队成员密切合作，以确保达到所需的质量水平。这包括与业务代表合作以帮助他们创建合适的验收测试，以及与开发人员合作以就测试策略达成一致并决定测试自动化方法。因此，测试人员可以将测试知识传授给其他团队成员并影响产品的开发。
根据具体情况，完整团队方法可能并不总是合适的。例如，在某些情况下，例如安全关键型，可能需要高水平的测试独立性。
40

---

<!-- Slide 41 -->

Question #8
How is the whole team approach present in the interactions between testers and business representatives?
a) Business representatives decide on test automation approaches
b) Testers help business representatives to define test strategy
c) Business representatives are not part of the whole team approach
d) Testers help business representatives to create suitable acceptance tests

41

---

<!-- Slide 42 -->

1.5.3. 	测试的独立性
由于作者和测试人员的认知偏差之间的差异，一定程度的独立性使测试人员更有效地发现缺陷（参见 Salman 1995）。然而，独立性并不能替代熟悉性，例如，开发人员可以有效地在自己的代码中发现许多缺陷。
**工作成果可以由作者（无独立性）、来自同一团队的作者同事（具有一定独立性）、来自作者团队外部但在组织内部的测试人员（高独立性）或来自组织外部的测试人员（非常高的独立性）进行测试。**
**对于大多数项目，通常最好执行具有多个独立性的测试（例如，开发人员执行组件测试和组件集成测试，测试团队执行系统和系统集成测试，业务代表执行验收测试）。**
独立测试的主要好处是，由于开发人员的背景、技术观点和偏见不同，独立测试人员可能会识别出不同类型的失败和缺陷。此外，独立测试人员可以验证、质疑或反驳利益相关者在系统规范和实施过程中所做的假设。
但是，也有一些缺点。独立测试人员可能与开发团队隔离开来，这可能会导致缺乏协作、沟通问题或与开发团队产生对抗关系。开发人员可能会失去对质量的责任感。独立测试人员可能会被视为瓶颈或被指责为发布延迟。
42

---
