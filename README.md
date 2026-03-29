# 马浩然-25322105-第二次人工智能编程作业
## 1. 任务拆解与 AI 协作策略
在编写代码之前，我先概览了任务的几个阶段。整个任务大概分为几个阶段。
步骤一，从创建学生名单开始做起，让ai帮我生成了了一个现代化的，更贴近真实的学生名单；
步骤二，构建数据模型，先定义Student类，然后实现文件读取功能，对名单的每一行解析成Student对象，并用字典存储；
步骤三，实现核心查找功能，先处理用户输入的异常转换，再验证数量是否合法，然后从学生列表中抽取不重复的随机样本；
步骤四，实现文件生成，使用random.shuffle将学生列表原地打乱，然后逐行写入“考场安排表”和“准考证”文件；
## 2. 核心 Prompt 迭代记录
初代prompt：AI虽然能够实现随机点名和生成名单功能，但是缺少数量合法检验，也没有使用try-except捕获异常
def random_call(self, count):
    """随机点名功能"""
    count = int(count)
    all_students = list(self.students.values())
    selected = random.sample(all_students, count)
    
    print("随机点名结果：")
    for i, student in enumerate(selected, 1):
        print(f"{i}. {student.name} ({student.student_id})")
    
    return selected
    我增加的约束条件：1.需要使用try-except处理用户输入非数字的异常情况；2.进行数量合法检验，数量不能小于等于0或者大于总人数；3.对于崩溃情况要给予使用者友好提示。
    优化后的prompt：AI的代码更加符合工程规范
    def random_call(self, count)
    try:
        count = int(count)
        
        if count <= 0:
            print(f"\n✗ 错误：点名人数必须大于0！")
            return []
        
        if count > self.total_count:
            print(f"\n✗ 错误：点名人数不能超过总人数 {self.total_count}！")
            return []
        
        all_students = list(self.students.values())
        selected = random.sample(all_students, count)
        
        print("\n" + "=" * 50)
        print(f"随机点名结果（共{count}人）：")
        print("=" * 50)
        for i, student in enumerate(selected, 1):
            print(f"{i:2d}. {student.name} ({student.student_id}) - {student.class_name} - {student.college}")
        print("=" * 50)
        
        return selected
        
    except ValueError:
        print(f"\n✗ 错误：请输入有效的数字！")
        return []
## 3. Debug 与异常处理记录
（记录一次解决报错或发现AI逻辑漏洞的过程） 报错类型/漏洞现象：...（如 FileNotFoundError 或 路径拼接错误） 解决过程：...（是我自己看懂了 Traceback 解决的，还是将报错喂给 AI 解决的？最终修改了哪里？）
## 4. 人工代码审查 (Code Review)
（请贴出一段 AI 生成的核心逻辑代码，并加上你自己的逐行中文注释，证明你完全理解了它的运行机制）```python
# 贴入代码及人工注释
