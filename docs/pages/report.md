# Course Report

```Python
@component()
class Course(Object):
    code = Attr(str, "HCI 1", enum=["HCI 1", "HCI 2", "HCI 3"])
    score = Attr(float, 0, min=0, max=15, step=1, hint="Enter final score (0-15)")
    remark = Attr(str, "Pending", enum=["Pending", "Pass", "Failed"], ro=True)
    eligible = State(["No", "Yes"])
    
    @transition(pre=["No"], post="Yes")
    def mark_passed(self):
        if self.score >= 12:
            self.remark = "Pass"
        else:
            raise ValueError("Cannot pass. Score must be at least 12.")
            
    def mark_failed(self):
        if self.score < 12:
            self.remark = "Failed"
        else:
            raise ValueError("Score is 12 or above, use 'mark_passed' instead.")


report = Course()

```
{: .inspector #report_widget }


```yaml
hci1 : 4
hci2 : 4
hci3 : 4
TotalScore:
```
{: .form #inputs editable="true" title="Grades"}

** {= `inputs.hci1` + `inputs.hci2`} **