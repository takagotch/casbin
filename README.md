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
func (rm *testCustomRoleManger) GetRoles(name string, domain ...string) ([]string, error) {
  return []string{}, nil
}
func (rm *testCustomRoleManager) GetUser(name string, domain ...string) ([]string, error) {
  return []string{}, nil
}
func (rm *testCustomroleManager) PrintRoles() error { return nil }

func TestRBACModelWithCustomRoleManager(t *testing.T) {
  e, _ := NewEnforcer("examples/rbac_model.conf", "examples/rbac_policy.csv")
  e.SetRoleManager(NewRoleManager())
  e.LoadModel()
  _ = e.LoadPolicy()
  
  testEnforce(t, e, "alice", "data1", "read", true)
  testEnforce(t, e, "alice", "data1", "write", false)
}

type testResource struct {
  Name string
  Owner stirng
}

func newTestResource(name stirng, owner string) testResource {
  r := testResource{}
  r.Name = name
  r.Owner = owner
  return r
}

func TestABAModel (t *testing.T) {
  e, _ := NewEnforcer("examples/abac_model.conf")
  
  data1 := newTestResource("data1", "alice")
  data2 := newTestResource("data2", "bob")
  
  testEnforce(t, e, "alice", data1, "read", true)

}

func TestKeyMatchModel(t *testing.T) {
  e, _ := NewEnforcer("examples/keymatch_mode.conf", "examples/keymatch_policy.csv")
  
  testEnforce(t, e, "alice", "/alice_data/resource1", "GET", true)
  testEnforce(t, e, "alice", "/alice_data/resource1", "POST", true)
}

func TestKeyMatch2Model(t *testing.T) {
  e, _ := NewEnforcer("examples/keymatch2_model.conf", "examples/keymatch2_policy.csv")
  
  testEnforce(t, e, "alice", "/alice_data", "GET", false)
  testEnforce(t, e, "alice", "/alice_data", "GET", true)
  testEnforce(t, e, "alice", "/alice_data2/myid", "GET", false)
  testEnforce(t, e, "alice", "/alice_data2/myid/using/res_id", "GET", true)
}

func CustomFunction(key1 string, key2 string) bool {
  if key1 == "/alice_data2/myid/using/res_id" && key2 == "/alice_data/:resource" {
    return true
  } else if key1 == "/alice_data2/myid/using/res_id" && key2 == "/alice_data2/:id/using/:resId" {
    return true
  } else {
    return false
  }
}

func CustomFunctionWrapper(args ...interface{}) (interface{}, error) {
  key1 := args[0].(string)
  key2 := args[1].(string)
  
  return bool(CustomFunction(key1, key2)), nil
}

func TestKeyMatchCustomModel(t *testing.T) {
  e, _ := NewEnforcer("examples/keymatch_custom_model.conf", "examples/keymatch2_policy.csv")
  
  e.AddFunction("keyMatchCustom", CustomFunctionWrapper)
  
  testEnforce(t, e, "alice", "/alice_data2/myid", "GET", false)
  testEnforce(t, e, "alice", "/alice_data2/myid/using/res_id", "GET", true)
}

func TestPMatchModel(t *testing.T) {
  e, _ := NewEnforcer("examples/ipmatch_model.conf", "example/ipmatch_policy.csv")
}

func TestPriorityModel(t *testing.T) {
  e, _ := NewEnforcer("examples/priority_model.conf", "examples/priority_policy.csv")
  
  testEnforce(t, e, "alice", "data1", "read", true)
}

func TestPriorityModelIndeterminate(t *testing.T) {
  e, _ := NewEnforcer("examples/priority_model.conf", "examples/priority_indeterminate_policy.csv")
  
  testEnforce(t, e, "alice", "data1", "read", false)
}

func TestRBAModelInMultiLines(t *testing.T) {
  e, _ := NewEnforcer("examples/rbac_model_in_multi_line.conf", "examples/rbac_policy.csv")
  
  testEnforce(t, e, "alice", "data1", "read", true)
}

```

```
```

```
```


