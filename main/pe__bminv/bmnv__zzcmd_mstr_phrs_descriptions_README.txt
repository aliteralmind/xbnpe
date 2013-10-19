--Syntax for a MINV-Command Master-Phrase's description--

This documentation uses this example MINV-Command:
   -Action name: pc2
   -MINV-Variable abbreviation: vphrd
   -MINV-Variable's internal-variable name: zvPHRASES_DOWN

If actions and the set-number-to-prompt-action are both on:
    pc2<...>#, pc2[{#insert zzMnvSynPstSetNumToPrompt},{#insert zzMnvSynPstCmdInfoSyntax},[[{#insert zzMnvSynPstNumSetphrsPreCallMstr},{#insert zzMnvSynPstSetToNumPreCallMstr}]]{#insert zzMnvSynPstMstrPhrsNm}], vphrd[[{#insert zzMnvSynPstMainPhrsCrtr},{#insert zzMnvSynPstVarInfoSyntax}]]
Otherwise:
    pc2<...>#, pc2[{#insert zzMnvSynPstCmdInfoSyntax},[[{#insert zzMnvSynPstNumSetphrsPreCallMstr},{#insert zzMnvSynPstSetToNumPreCallMstr}]]{#insert zzMnvSynPstMstrPhrsNm}], vphrd[[{#insert zzMnvSynPstMainPhrsCrtr},{#insert zzMnvSynPstVarInfoSyntax}]]

where <...> is one of the following:

   Key:
      -ACT=Actions on or off?  (zvACTIONS_ON)
      -sntpa=Set-Number-To-Prompt action (zvSNTP_ACTN_ON)
      -PC=Phrase-Creators on or off?  (zvPHRS_CRTRS_ON)
      -p/es=Phrase-creator postfix '{#insert zzMnvSynPstMainPhrsCrtr}' or '' (empty-string)? (zvPCAF_PST_PORES)
      -ltry=Literal phrase-creator style: off/on (zvLTRL_STYL_ESYC) ['on' simply means NOT off--curly or command]

   Notes:
      -sntpa is not applicable when actions (act) are OFF
      -ltry is not applicable when phrase-creators are OFF
      -p/es is not applicable unless phrase-creators are ON and actions are OFF

****************Change 'p' to {#insert zzMnvSynPstMainPhrsCrtr} and 'q' to {#insert zzMnvSynPstLtrlPhrsCrtr}
   ACT  sntpa      PC   p/es  ltry            SYNTAX
   -------------------------------            ------
   on    on        on         off             [[n,p]]
   on    on        on         on              [[n,p,q]]
   on    on        off                        [n]
   on    off       on         off             [p]
   on    off       on         on              [[p,q]]
   on    off       off                        ''
   off             on    p    off             p
   off             on    p    on              [p,q]
   off             on    ''   off             *
   off             on    ''   on              [*,p]
   off             off                        n/a (post-actm-syntax phrases never called)

(The asterisk, '*', indicates that the phrase-creator has no postfix--it is equal to the action name. Since this is only possible when actions are OFF, this is not a conflict. This is reiterated in the master-phrase's body comment.)

These are all possible commands, some of which are not available, depending on the above syntax (note that a number between [CmdRangeMin] and [CmdRangeMax] can be appended where '#' is printed below--and when [NoNumAlias_onff] is ON, then NO NUMBER is also legal in its place):
   -pc2#: Run action (if actions are off and the pc-postfix is '', then this is the phrase-creator)
   -pc2{#insert zzMnvSynPstMainPhrsCrtr}}#: Prints a CALL to the command, when phrase-creators are on, and '{#insert zzMnvSynPstMainPhrsCrtr}' is the phrase-creator postfix. When commands are off, this is instead equivalent to 'pc2{#insert zzMnvSynPstSetToNumCallMstr}'
   -pc2{#insert zzMnvSynPstSetNumToPrompt}: Run the set-number-to-prompt action
   -pc2{#insert zzMnvSynPstCmdInfoSyntax}: Prints the MINV-Variable's interval-variable name, and its syntax (the same as in the master-phrase description: vphrd[{#insert zzMnvSynPstMainPhrsCrtr},{#insert zzMnvSynPstVarInfoSyntax}])
   -pc2{#insert zzMnvSynPstSetToNumCallMstr}: Prints a call to zvPHRASES_DOWN_st[prompt], master-phrase-name
   -pc2{#insert zzMnvSynPstSetToNumCallMstr}: Prints a call to zvPHRASES_DOWN_st[prompt], master-phrase-name
   -pc2{#insert zzMnvSynPstMstrPhrsNm}: Prints a call to the master-phrase-name
   -vphrd: Prints the VALUE of the MINV-Variable (for diagnostics)
   -vphrd{#insert zzMnvSynPstMainPhrsCrtr}: Prints a CALL to the MINV-Variable: {#insert zOY}#insert zvPHRASES_DOWN{#insert zCY}
   -vphrd{#insert zzMnvSynPstVarInfoSyntax}: Prints the NAME of the MINV-Variable: zvPHRASES_DOWN
