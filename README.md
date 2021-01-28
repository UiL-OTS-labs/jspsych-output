# jspsych-output
A short description of the output of jsPsych

## Introduction

This is a short introduction to the output generated by jsPsych experiments. jsPsych 
is the software used by researchers in the Uil OTS labs to run online experiments. 

jsPsych comes with its internal "database" for the research data that is collected during one run of
the experiment. jsPsych is rather verbose in its output, and everything
that is presented to the participant is treated as a single trial. This means
that for instance the fixation cross
that starts your trial is - in the output of jsPsych - a trial of its own. This
is not ideal, but it is how jsPsych works internally.

This document explains where you can find the relevant documentation in
the jsPsych documentation to understand the output that is generated by your
experiment. We provide the relevant links and a little guidance in order to
understand the output.

## jsPsych general trial information
Each jsPsych trial is started via a jsPsych plugin. All plugins will write the
following four variables to the output:

1. **trial_type**
2. **trial_index**
3. **time_elapsed**
4. **internal_node_id**

Information can be obtained from the [data-collected-from-plugins][1] section in the
jsPsych documentation. The most significant variable is the first, **trial_type**
because that determines where you can look for the meaning of the other variables of
the same jsPsych trial. For example, in a visual lexical decision task with a visual
prime, a trials starts with a fixation cross, then a prime and then a (non-)word
again. In terms of jsPscych those are 3 trials. the cross, the prime and the
(non-)word. They are all presented with the same plugin called:
*html-keyboard-response*. In order to see the meaning of the other variables
you'll have to look up the plugin of that trial in the [list of plugins][2]. All
the plugins are prefixed with "jspsych-", so you'll be looking for the plugin:
*jspsych-html-keyboard-response*. Once you have found it, you need to
look for the paragraph *Data Generated*. In the panel on the right hand side
of the web page you can find a link to the section.
There are 3 variables listed:

1. **key_press**
2. **rt**
3. **stimulus**

So for the html-keyboard-response-plugin, in addition to the 4 variables above, the
**key_press**, **rt** and **stimulus** are stored in the output. As you can see,
the type and meaning of the variable are also listed in the table.

## Data added by the boilerplates of the UiL OTS labs
Scripts using jsPsych can add some own data to each trial. The UiL OTS
boilerplate experiments also add some variables in the hope they are useful for
analyzing the experiment data.

In addition to the 7 variables (in the case of the html-keyboard-response) above,
the boilerplate experiments of the UiL OTS labs add two additional
variables to each trial. This is done for example by:

```javascript
jsPsych.data.addProperties (
    {
        subject : subject_id,
        list : list_name
    }
);
```
The two variables added by the experiment script are:

1. **subject** A random id generated when the experiment starts.
2. **list** The chosen list from the available lists in the experiment.

## Experiment specific variables

Different experiments need different output. The UiL OTS Self Paced Reading
(SPR) boilerplate  for example records up to 15 reaction times per trial, 
whereas the lexical decision (LD) templates only record one.
You'll have to look this up in the documentation of each boilerplate.

[1]:<https://www.jspsych.org/plugins/overview/#data-collected-by-plugins>
[2]:<https://www.jspsych.org/plugins/overview/#list-of-available-plugins>

