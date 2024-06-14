
LIMIT RULES

**Do not enable every AIE Rule.**While it may be tempting to enable every rule in an AI Engine arsenal, it is **strongly encouraged to refrain from doing so**. Every AIE Rule carries a certain level of processing and memory requirements – to enable all rules is to invite maximum usage of system resources for any rule that requires them. 

Because every environment is different (due to different log sources and technologies), it is a better idea to **selectively choose** which ones you want to enable and **ensure that filtering is updated** to fit your environment's needs.

Even if you find a **prepackaged AIE Rule** that you like, it is recommended to clone and update it to meet your needs: Select the rule's action box > right click > clone > rename > customize to better fit your environment. 

Note: Simply enabling a prepackaged rule without cloning it means you'll be limited in how you can edit it. In addition, every time the Knowledge Base updates—about once a week—any changes you _were_ able to make could be overwritten by the update.



MAKE IT APPLICABLE

**Limit Log Source Criteria for AIE Rules to applicable log sources only.**

- Not every rule block configuration requires examination of all logs. As mentioned in a previous section, it is unlikely that AI Engine will require monitoring of all logs from all devices for all rules as many logs will never meet rule criteria. Thus, AI Engine will be unnecessarily taxed on resources.  
    
- Log Source Criteria is examined per rule block, not per rule. In other words (and referencing the first recommendation), if Log Source Criteria for every AIE Rule includes all log sources, multiple instances of this criteria will be present for multi-block AIE Rules, furthering excessive resource consumption. Multiplied over all enabled rules, this is an unsustainable AI Engine configuration.


USE DEDICATED WORKLOADS

**Consider creating a dedicated workload for enabled rules.**

Even a disabled AI Engine Rule uses 0.5MB (or 500K) of memory. While one disabled rule will not severely impact performance, a large collection of disabled rules from one module has this potential. 

Because of this, LogRhythm recommends a **dedicated workload** that contains only the enabled rules of an environment. To do this:

1. Create a **workload** and **rules set** (see steps above). 
2. **Include an "Active Rules" rule set in a workload** by:
    1. Selecting the action box of the rules set in the Rules Set section of the Workloads tab, 
    2. Right-clicking within the grid and selecting "Include in Workload."
    3. Selecting OK in the Include Rules Sets message that appears.

