### Docker Hub
```bash
https://hub.docker.com/repository/docker/pritomssaha/601_module10/
```
<img src="/assets/docker_hub.PNG" />

### GitHub workflow
<img src="/assets/github_workflow.PNG" />

### clone the repo
```bash
git clone git@github.com:pritomssaha/IS601_module_10.git
```
### start the virtual env
```bash
python3 -m venv venv
source venv/bin/activate
````
### install dependency
```bash
pip3 install -r requirements.txt
```
#### run the pytest
```bash
(venv) pritom@DESKTOP-8L8AR1I:~/module10_is601$ pytest
============================================================================= test session starts =============================================================================
platform linux -- Python 3.12.3, pytest-8.3.3, pluggy-1.5.0
rootdir: /home/pritom/module10_is601
configfile: pytest.ini
testpaths: tests
plugins: Faker-33.3.0, cov-6.0.0, pylint-0.21.0, anyio-4.6.2.post1
collected 75 items                                                                                                                                                            

tests/e2e/test_e2e.py ...                                                                                                                                               [  4%]
tests/integration/test_database.py ....                                                                                                                                 [  9%]
tests/integration/test_dependencies.py .....                                                                                                                            [ 16%]
tests/integration/test_fastapi_calculator.py .....                                                                                                                      [ 22%]
tests/integration/test_schema_base.py ............                                                                                                                      [ 38%]
tests/integration/test_user.py ........s....                                                                                                                            [ 56%]
tests/integration/test_user_auth.py ............                                                                                                                        [ 72%]
tests/unit/test_calculator.py .....................                                                                                                                     [100%]

---------- coverage: platform linux, python 3.12.3-final-0 -----------
Name                         Stmts   Miss  Cover   Missing
----------------------------------------------------------
app/__init__.py                  0      0   100%
app/auth/__init__.py             0      0   100%
app/auth/dependencies.py        18      0   100%
app/config.py                    6      0   100%
app/database.py                 21      4    81%   60-64
app/database_init.py             7      0   100%
app/models/__init__.py           0      0   100%
app/models/user.py              77      0   100%
app/operations/__init__.py      16      0   100%
app/schemas/__init__.py          3      0   100%
app/schemas/base.py             30      0   100%
app/schemas/user.py             26      0   100%
----------------------------------------------------------
TOTAL                          204      4    98%
Coverage HTML written to dir htmlcov


======================================================================== 74 passed, 1 skipped in 7.55s ========================================================================
```
### Start the Docker container
```bash
docker compose up --build
```
### Once the Docker build is complete, set up the pgadmin
### Now run this command to test test_user with preserve DB
```bash
pytest -s -v tests/integration/test_user.py --preserve-db
```
### check test user data is inserted by running this query, if the count is 0, data is not inserted
```sql
select count(1) as "Total_count" from users
```
<table>   
   <tr>
      <th>Total_count</th>
   </tr>
   <tr>
      <td>15</td>
   </tr>
</table>

### Drop the table by running the command
```sql
drop table users
```
### Now test the schema base
```bash
pytest -s -v tests/integration/test_schema_base.py --preserve-db
```
```bash
2026-04-07 22:39:28,293 - tests.conftest - INFO - Initialized the test database with initial data. PASSED
tests/integration/test_schema_base.py::test_user_base_invalid_email PASSED
tests/integration/test_schema_base.py::test_password_mixin_valid PASSED
tests/integration/test_schema_base.py::test_password_mixin_invalid_short_password PASSED
tests/integration/test_schema_base.py::test_password_mixin_no_uppercase PASSED
tests/integration/test_schema_base.py::test_password_mixin_no_lowercase PASSED
tests/integration/test_schema_base.py::test_password_mixin_no_digit PASSED
tests/integration/test_schema_base.py::test_user_create_valid PASSED
tests/integration/test_schema_base.py::test_user_create_invalid_password PASSED
tests/integration/test_schema_base.py::test_user_login_valid PASSED
tests/integration/test_schema_base.py::test_user_login_invalid_username PASSED
tests/integration/test_schema_base.py::test_user_login_invalid_password PASSED2026-04-07 22:39:28,389 - tests.conftest - INFO - Skipping drop_db due to --preserve-db flag.
```
### Drop the table by running the command
```sql
drop table users
```
### Now test the user auth application
```bash
pytest -s -v tests/integration/test_user_auth.py --preserve-db
```
### check test user data is inserted by running this query, if the count is 0, data is not inserted
```sql
select count(1) as "Total_count" from users
```
<table>   
   <tr>
      <th>Total_count</th>
   </tr>
   <tr>
      <td>8</td>
   </tr>
</table>



