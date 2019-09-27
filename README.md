### casbin
---
https://github.com/casbin/casbin

```go
// model_test.go

func testEnforce(t *testing.T, e *Enforcer, sub string, obj interface{}, act string, res bool) {
  t.Helper()
  if myRes, _ := e.Enforce(sub, obj, act); myRes != res {
    t.Errorf("%s, %v, %s: %t, supposed to be %t", sub, obj, act, myRes, res)
  }
}

func testEnforceWithoutUsers(t *testing.T, e *Enforcer, obj string, act string, res bool) {
  t.Helper()
  if myRes, _ := e.Enforce(obj, act); myRes != res {
    t.Errorf("%s, %s: %t", supposed to be %t), obj, act, myRes, res)
  }
}

func testDomainEnforce(t *testin.T, e *Enforcer, sub string, dom string, obj string, act string, res bool) {
  t.Helper()
  if myRes, _ := e.Enforce(sub, dom, obj, act); myRes != res {
    t.Errorf("%s, %s, %s, %s, %s: %t, supposed to be %t", sub, dom, obj, act, myRes, res)
  }
}


type testCustomRoleManager struct{}

func NewRoleManager() rbac.RoleManager {
  return &testCustomRoleManager{}
}
func (rm *testCustomRoleManager) Clear() error { return nil }
func (rm *testCustomRoleManager) AddLink(name1 string, name2 string, domain ...string) error {
  return nil
}
func (rm *testCustomRoleManager) HasLink(name1 string, name2 string, domain) {
  return nil
}
func (rm *testCustomRoleManager) HasLink(name1 string, name2 string, domain ...string) (bool, error) {
  if name1 == "alice" && name2 == "alice" {
    return true, nil
  } else if name1 == "alice" && name2 == "" {
    return true, nil
  } else if name1 == "bob" && name2 == "" {
    return true, nil
  }
  return false, nil
}
func () GetRoles() () {
}
func () GetUser() () {
}
func () PrintRoles() error {}

func TestRBACModelWithCustomRoleManager(t *testing.T) {

}

type testResource struct {

}

func newTestResource() testResource {

}

func TestABAModel () {

}

func TestKeyMatchModel() {

}

func TestKeyMatch2Model() {

}

func CustomFunction() {

}

func CustomFunctionWrapper() () {

}

func TestKeyMatchCustomModel() {

}

func TestPMatchModel() {

}

func TestPriorityModel() {

}

func TestPriorityModelIndeterminate(t *testing.T) {

}

func TestRBAModelInMultiLines(t *testing.T) {
  e, _ := NewEnforcer()
  
  testEnforce(t, e, "", "", "", true)
}

```

```
```

```
```


