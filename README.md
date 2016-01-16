;# AutoitRoulette1
;A Roulette simulation to try our various strategies on outside table bets


;A roullete simulation or player that can be used to 'simulate' the spins of roulette
;with the user betting on outside bets eg, Red or Black, 1st Doz, 2nd Doz etc.

;Here's the Autoit code, needs more Tool tips and a few other bits, but seems to work pretty 
;well and should be largely self explanatory.
;An on going project.

;*******************************************************
;*******************************************************
;*******************************************************



#include <ButtonConstants.au3>
#include <EditConstants.au3>
#include <GUIConstantsEx.au3>
#include <ProgressConstants.au3>
#include <StaticConstants.au3>
#include <WindowsConstants.au3>
#include <ColorConstants.au3>
#include <MsgBoxConstants.au3>


#include <GUIToolTip.au3>
;#include <StaticConstants.au3>
Opt("GUIOnEventMode", 0)
Opt("GUICloseOnESC", 1) ;1=ESC  closes, 0=ESC won't close

;***************************************************************

#include <ButtonConstants.au3>
#include <EditConstants.au3>
#include <GUIConstantsEx.au3>
#include <ProgressConstants.au3>
#include <StaticConstants.au3>
#include <WindowsConstants.au3>
#Region ### START Koda GUI section ### Form=
$Form1_1 = GUICreate("RouletteSimAde1", 526, 540, 333, 144)
$Button1 = GUICtrlCreateButton("Red", 60, 60, 70, 31)
$Button2 = GUICtrlCreateButton("Black", 60, 90, 70, 31)
$Button3 = GUICtrlCreateButton("Odd", 60, 130, 70, 31)
$Button4 = GUICtrlCreateButton("Even", 60, 160, 70, 31)
$Button5 = GUICtrlCreateButton("1 - 18", 60, 200, 70, 31)
$Button6 = GUICtrlCreateButton("19 - 36", 60, 230, 70, 31)
$Button7 = GUICtrlCreateButton("1st 12", 60, 270, 70, 31)
$Button8 = GUICtrlCreateButton("2nd 12", 60, 300, 70, 31)
$Button9 = GUICtrlCreateButton("3rd 12", 60, 330, 70, 31)
$Button10 = GUICtrlCreateButton("Row 1", 62, 373, 70, 31)
$Button11 = GUICtrlCreateButton("Row 2", 62, 403, 70, 31)
$Button12 = GUICtrlCreateButton("Row 3", 62, 433, 70, 31)
$Checkbox1 = GUICtrlCreateCheckbox("Grp1", 10, 90, 40, 31)
$Checkbox2 = GUICtrlCreateCheckbox("Grp2", 10, 160, 41, 31)
$Checkbox3 = GUICtrlCreateCheckbox("Grp3", 10, 230, 41, 31)
$Checkbox4 = GUICtrlCreateCheckbox("Grp4", 10, 330, 40, 31)
$Checkbox5 = GUICtrlCreateCheckbox("Grp5", 10, 430, 41, 31)
$Group1 = GUICtrlCreateGroup("Simulation Mode", 10, 470, 195, 51)
$Radio1 = GUICtrlCreateRadio("Step", 20, 490, 71, 21)
$Radio2 = GUICtrlCreateRadio("Free Running", 100, 490, 80, 21)
GUICtrlCreateGroup("", -99, -99, 1, 1)
$Button13 = GUICtrlCreateButton("Simulate", 390, 470, 60, 30)
$Button14 = GUICtrlCreateButton("Sngl Spin", 390, 500, 60, 30)
$Button15 = GUICtrlCreateButton("Exit", 450, 500, 60, 30)
GUICtrlSetFont(-1, 8, 800, 0, "MS Sans Serif")
$Button16 = GUICtrlCreateButton("Reset", 450, 470, 60, 30)
$Label1 = GUICtrlCreateLabel("Bankroll", 80, 10, 42, 17)
$Label2 = GUICtrlCreateLabel("Spins", 10, 10, 30, 17)
$Label3 = GUICtrlCreateLabel("Threshold", 150, 10, 51, 17)
$Label4 = GUICtrlCreateLabel("Stop Loss", 220, 10, 51, 17)
$Label5 = GUICtrlCreateLabel("Table Limit", 290, 10, 66, 17)
$Label7 = GUICtrlCreateLabel("Bet Size", 432, 10, 66, 17)
$Label6 = GUICtrlCreateLabel("Target BR", 360, 10, 66, 17)
$Label8 = GUICtrlCreateLabel("0", 440, 66, 55, 54)
GUICtrlSetFont(-1, 36, 800, 0, "Impact")
GUICtrlSetColor(-1, 0x000000)
$Input1 = GUICtrlCreateInput("1000", 10, 30, 61, 21, BitOR($GUI_SS_DEFAULT_INPUT,$WS_BORDER), BitOR($WS_EX_CLIENTEDGE,$WS_EX_STATICEDGE))
GUICtrlSetBkColor(-1, 0xEEEEEE)
$Input2 = GUICtrlCreateInput("100", 80, 30, 61, 21, BitOR($GUI_SS_DEFAULT_INPUT,$WS_BORDER))
GUICtrlSetBkColor(-1, 0xEEEEEE)
$Input3 = GUICtrlCreateInput("5", 150, 30, 61, 21, BitOR($GUI_SS_DEFAULT_INPUT,$WS_BORDER))
GUICtrlSetBkColor(-1, 0xEEEEEE)
$Input4 = GUICtrlCreateInput("5", 220, 30, 61, 21, BitOR($GUI_SS_DEFAULT_INPUT,$WS_BORDER))
GUICtrlSetBkColor(-1, 0xEEEEEE)
$Input5 = GUICtrlCreateInput("250", 290, 30, 61, 21, BitOR($GUI_SS_DEFAULT_INPUT,$WS_BORDER))
GUICtrlSetBkColor(-1, 0xEEEEEE)
$Input6 = GUICtrlCreateInput("1", 360, 30, 61, 21, BitOR($GUI_SS_DEFAULT_INPUT,$WS_BORDER))
GUICtrlSetBkColor(-1, 0xEEEEEE)
$Input7 = GUICtrlCreateInput("1", 430, 30, 61, 21, BitOR($GUI_SS_DEFAULT_INPUT,$WS_BORDER))
GUICtrlSetBkColor(-1, 0xEEEEEE)
$Progress1 = GUICtrlCreateProgress(140, 70, 261, 11)
GUICtrlSetTip(-1, "/5")
$Progress2 = GUICtrlCreateProgress(140, 100, 261, 11)
GUICtrlSetTip(-1, "/5")
$Progress3 = GUICtrlCreateProgress(140, 140, 261, 11)
GUICtrlSetTip(-1, "/5")
$Progress4 = GUICtrlCreateProgress(140, 170, 261, 11)
GUICtrlSetTip(-1, "/5")
$Progress5 = GUICtrlCreateProgress(140, 210, 261, 11)
GUICtrlSetTip(-1, "/5")
$Progress6 = GUICtrlCreateProgress(140, 240, 261, 11)
GUICtrlSetTip(-1, "/5")
$Progress7 = GUICtrlCreateProgress(140, 280, 261, 11)
GUICtrlSetTip(-1, "/5")
$Progress8 = GUICtrlCreateProgress(140, 310, 261, 11)
GUICtrlSetTip(-1, "/5")
$Progress9 = GUICtrlCreateProgress(140, 340, 261, 11)
GUICtrlSetTip(-1, "/5")
$Progress10 = GUICtrlCreateProgress(140, 380, 261, 11)
GUICtrlSetTip(-1, "/5")
$Progress11 = GUICtrlCreateProgress(140, 410, 261, 11)
GUICtrlSetTip(-1, "/5")
$Progress12 = GUICtrlCreateProgress(140, 440, 261, 11)
GUICtrlSetTip(-1, "/5")
$Button17 = GUICtrlCreateButton("Unused", 329, 499, 60, 30)
$Button18 = GUICtrlCreateButton("Unused", 330, 470, 60, 30)
$Button19 = GUICtrlCreateButton("Unused", 270, 470, 60, 30)
$Button20 = GUICtrlCreateButton("Unused", 270, 500, 60, 30)
$Pic1 = GUICtrlCreatePic("", 424, 384, 89, 73)
$Pic2 = GUICtrlCreatePic("", 424, 288, 89, 81)
$Label9 = GUICtrlCreateLabel("Spare Data 09", 424, 144, 84, 17)
$Labe10 = GUICtrlCreateLabel("Spare Data 10", 424, 168, 84, 17)
$Labe11 = GUICtrlCreateLabel("Spare Data 11", 424, 192, 84, 17)
$Labe12 = GUICtrlCreateLabel("Spare Data 12", 424, 216, 84, 17)
GUISetState(@SW_SHOW)
#EndRegion ### END Koda GUI section ###



;****************************************************************






















;#EndRegion ### END Koda GUI section ###
Local $hToolTip
Local $Nmbr = 0
Local $SpinNo = 0
Local $Spins = 5000
Local $BetRed = 0
Local $BetBlack = 0
Local $BetOdd = 0
Local $BetEven = 0
Local $Bet1To18 = 0
Local $Bet19To36 = 0
Local $Bet1stDoz = 0
Local $Bet2ndDoz = 0
Local $Bet3rdDoz = 0
Local $BetRow1 = 0
Local $BetRow2 = 0
Local $BetRow3 = 0
Local $Loss1 = 0
Local $Loss2 = 0
Local $CurrentBR = 0
Local $MaxBR = 0
Local $NewTargetBR = 0
Local $BetSize = 1
Local $StartBankRoll = 0
Local $StopLoss
Local $Bet1st
Local $BetAmount = 0
Local $Threshld = 0
GUISetState(@SW_SHOW)
Local $CurrentBR = Number(GUICtrlRead($Input2))
$StartBankRoll = $CurrentBR
$CurrentBR = GUICtrlRead($Input2)
$MaxBR = $CurrentBR
$NewTargetBR = $MaxBR
GUICtrlSetData($Input6, $CurrentBR)

;_GUIToolTip_AddTool($hToolTip, 0, "This tooltip belongs to the button", $Button6)
;_GUIToolTip_AddTool($hToolTip, $hGUI, "Upper Left corner", 0, 10, 10, 168, 85, $TTF_SUBCLASS
GUICtrlSetData($Progress1, 10)
GUICtrlSetData($Progress2, 10)
GUICtrlSetData($Progress3, 10)
GUICtrlSetData($Progress4, 10)
GUICtrlSetData($Progress5, 10)
GUICtrlSetData($Progress6, 10)
GUICtrlSetData($Progress7, 10)
GUICtrlSetData($Progress8, 10)
GUICtrlSetData($Progress9, 10)
GUICtrlSetData($Progress10, 10)
GUICtrlSetData($Progress11, 10)
GUICtrlSetData($Progress12, 10)
GUICtrlSetData($Input1, 100)
GUICtrlSetData($Input2, 100)
GUICtrlSetData($Input3, 5)
GUICtrlSetData($Input4, 5)
GUICtrlSetData($Input5, 250)

 GUICtrlSetState($Checkbox1, 1) ; checked
 GUICtrlSetState($Checkbox2, 1) ; checked
  GUICtrlSetState($Checkbox3, 1) ; checked
   GUICtrlSetState($Checkbox4, 1) ; checked
    GUICtrlSetState($Checkbox5, 1) ; checked

Call ("Sim1")

While 1
	$nMsg = GUIGetMsg()
$CurrentBR = Number(GUICtrlRead($Input2))
$BetSize = 1
Switch $nMsg


	Case $Button1
		If ( GUICtrlRead($Checkbox1) = 1) Then  ; If Grp is checked)
												; Then we can bet 1 unit if Button is clicked.
		$BetSize = 1
			If $CurrentBR > 0 Then
				$BetRed += 1
				Call("BankRoll" , $BetSize)
			EndIf
		EndIf

	Case $Button2
		If ( GUICtrlRead($Checkbox1) = 1) Then  ; If Grp is checked)
		   												; Then we can bet 1 unit if Button is clicked.

		$BetSize = 1
			If $CurrentBR > 0 Then
				$BetBlack += 1
				Call("BankRoll", $BetSize)
			EndIf
		EndIf

	Case $Button3
		If ( GUICtrlRead($Checkbox2) = 1) Then  ; If Grp is checked)
		   												; Then we can bet 1 unit if Button is clicked.

		$BetSize = 1
			If $CurrentBR > 0 Then
				$BetOdd += 1
				Call("BankRoll", $BetSize)
			EndIf
		EndIf

	Case $Button4
		If ( GUICtrlRead($Checkbox2) = 1) Then  ; If Grp is checked)
		   												; Then we can bet 1 unit if Button is clicked.

		$BetSize = 1
			If $CurrentBR > 0 Then
				$BetEven += 1
				Call("BankRoll", $BetSize)
			EndIf
		EndIf


	Case $Button5
		If ( GUICtrlRead($Checkbox3) = 1) Then  ; If Grp is checked)
		   												; Then we can bet 1 unit if Button is clicked.

		$BetSize = 1
			If $CurrentBR > 0 Then
				$Bet1To18 += 1
				Call("BankRoll", $BetSize)
			EndIf
		EndIf

	Case $Button6
		If ( GUICtrlRead($Checkbox3) = 1) Then  ; If Grp is checked)
		   												; Then we can bet 1 unit if Button is clicked.

		$BetSize = 1
			If $CurrentBR > 0 Then
				$Bet19To36 += 1
				Call("BankRoll", $BetSize)
			EndIf
		EndIf


	Case $Button7
		If ( GUICtrlRead($Checkbox4) = 1) Then  ; If Grp is checked)
		   												; Then we can bet 1 unit if Button is clicked.

		$BetSize = 1
			If $CurrentBR > 0 Then
				$Bet1stDoz += 1
				Call("BankRoll", $BetSize)
			EndIf
		EndIf

		Case $Button8
		If ( GUICtrlRead($Checkbox4) = 1) Then  ; If Grp is checked)
		   												; Then we can bet 1 unit if Button is clicked.


		$BetSize = 1
			If $CurrentBR > 0 Then
				$Bet2ndDoz += 1
				Call("BankRoll", $BetSize)
			EndIf
		EndIf


			Case $Button9
		If ( GUICtrlRead($Checkbox4) = 1) Then  ; If Grp is checked)
		   												; Then we can bet 1 unit if Button is clicked.


		$BetSize = 1
			If $CurrentBR > 0 Then
				$Bet3rdDoz += 1
				Call("BankRoll", $BetSize)
			EndIf
		EndIf

	Case $Button10
	If ( GUICtrlRead($Checkbox5) = 1) Then  ; If Grp is checked)
	   												; Then we can bet 1 unit if Button is clicked.


		$BetSize = 1
			If $CurrentBR > 0 Then
				$BetRow1 += 1
				Call("BankRoll", $BetSize)
			EndIf
	EndIf

		Case $Button11
		If ( GUICtrlRead($Checkbox5) = 1) Then  ; If Grp is checked)
		   												; Then we can bet 1 unit if Button is clicked.


		$BetSize = 1
			If $CurrentBR > 0 Then
				$BetRow2 += 1
				Call("BankRoll", $BetSize)
			EndIf
		EndIf

			Case $Button12
		If ( GUICtrlRead($Checkbox5) = 1) Then  ; If Grp is checked)
		   												; Then we can bet 1 unit if Button is clicked.


		$BetSize = 1
			If $CurrentBR > 0 Then
				$BetRow3 += 1
				Call("BankRoll", $BetSize)
			EndIf
		EndIf


		Case $Button14				;Sngl Spin button pressed
			Call("Sim1")

	Case $Button16					;reset button pressed
		GUICtrlSetData ($Input1,1000) ;Default No of Spins
		GUICtrlSetData ($Input2,200) ;Default BankRoll
		GUICtrlSetData ($Input3,2) ;Default Threshold (IE No of times a Grp has NOT been seen
		GUICtrlSetData ($Input4,2) ;Stop Loss IE To how much are we prepared to progressively increase our bets to recover prior losses
		GUICtrlSetData ($Input6,200) ;Initially set to initial bankroll, will change in response to gains and stop loss
		GUICtrlSetData ($Input7,1) ;Initially we only wish to risk 1 bet on each set on numbers.


	Case $Button15			;Quit button pressed				
		Exit
		Case $Button13		;Sim Button Pressed
			$Spins = Number(GUICtrlRead($Input1))


			Call("Sim2")
	EndSwitch
WEnd
Func Sim1()
	;Local $iIdleTime = _Timer_GetIdleTime()
	;SRandom($tagFILETIME )


	;For $SpinNo = 1 to $Spins
	$Nmbr = Random(0, 36, 1)
	;MouseMove(Random(0,150,0),(Random(0,150,0)),1)
	If $Nmbr = 0 Then			; If Zero, Make Label Green
	GUICtrlSetColor ($Label8, 0x00ff00)
EndIf
;If $CurrentBR > $BetSize Then
	Call("Update")			;Update our winnings
;EndIf
	;Next
	GUICtrlSetData($Label8, $Nmbr)		;Show the number
	;Sleep(1)
	;Return
EndFunc   ;==>Sim1

;********* Simulate function ***************************
Func Sim2()
;*******Get reqd no of spins *****************
	$Spins = Number(GUICtrlRead($Input1))			;Get how many spins for he simulation run

	For $SpinNo = 1 To $Spins
		$Nmbr = Random(0, 36, 1)
		GUICtrlSetData($Input1,$Spins-$SpinNo)		;Turn label 1 in to a count down spin counter

;********** Display Rnd Numb **********
GUICtrlSetData($Label8, $Nmbr)

;********* If it's zero, make it Green *****************
If $Nmbr = 0 Then
	;Beep(5000, 100)


	GUICtrlSetColor ($Label8, 0x00ff00)
EndIf

If $CurrentBR > $BetSize Then			;If we have enough Bankroll to bet the Betsize amount

		Call ("Threshold")				; Is the Threshold = to or bigger than our setting
									   ;Threshold is the number of times a group has NOT been seen
EndIf

If ($CurrentBR < 1) Then				; If Bankroll is zero or less make sure it's zero
	$CurrentBR = 0

	EndIf
	GUICtrlSetData($Input2, $CurrentBR)		;Update the Bankroll

	;	Call("BankRoll")
		Call("Update")
		Sleep(1)
		;MsgBox($MB_SYSTEMMODAL, "Title", $BetBlack,$BetRed, 2)

	Next
	$BetSize = 1
		GUICtrlSetData($Input1,$Spins)

EndFunc

Func Update()
	;Update our winnings or losses dependong on the random number generated.
	If ($Nmbr = 1) Or ($Nmbr = 3) Or ($Nmbr = 5) Or ($Nmbr = 7) Or ($Nmbr = 9) Or ($Nmbr = 12) Or ($Nmbr = 14) Or ($Nmbr = 16) Or ($Nmbr = 18) Or ($Nmbr = 19) Or ($Nmbr = 21) Or ($Nmbr = 23) Or ($Nmbr = 25) Or ($Nmbr = 27) Or ($Nmbr = 30) Or ($Nmbr = 32) Or ($Nmbr = 34) Or ($Nmbr = 36) Then
		GUICtrlSetData($Progress2, 5 + Number(GUICtrlRead($Progress2))); Update progress bars which show how many times a group has NOT been seen
																		;Of course there is no memory in Roulette
		GUICtrlSetData($Progress1, 0)
		$CurrentBR = $CurrentBR + (2 * $BetRed)
		GUICtrlSetData($Input2, $CurrentBR)
		GUICtrlSetColor ($Label8, 0xff0000)
		$BetRed = 0
		$BetBlack = 0
	EndIf
	If ($Nmbr = 2) Or ($Nmbr = 4) Or ($Nmbr = 6) Or ($Nmbr = 8) Or ($Nmbr = 10) Or ($Nmbr = 11) Or ($Nmbr = 13) Or ($Nmbr = 15) Or ($Nmbr = 17) Or ($Nmbr = 20) Or ($Nmbr = 22) Or ($Nmbr = 24) Or ($Nmbr = 26) Or ($Nmbr = 28) Or ($Nmbr = 29) Or ($Nmbr = 31) Or ($Nmbr = 33) Or ($Nmbr = 35) Then
		GUICtrlSetData($Progress1, 5 + Number(GUICtrlRead($Progress1)))
		GUICtrlSetData($Progress2, 0)
		$CurrentBR = $CurrentBR + (2 * $BetBlack)
		GUICtrlSetData($Input2, $CurrentBR)
		GUICtrlSetColor ($Label8, 0x000000)
		$BetBlack = 0
		$BetRed = 0
	EndIf
	If ($Nmbr = 1) Or ($Nmbr = 3) Or ($Nmbr = 5) Or ($Nmbr = 7) Or ($Nmbr = 9) Or ($Nmbr = 11) Or ($Nmbr = 13) Or ($Nmbr = 15) Or ($Nmbr = 17) Or ($Nmbr = 19) Or ($Nmbr = 21) Or ($Nmbr = 23) Or ($Nmbr = 25) Or ($Nmbr = 27) Or ($Nmbr = 29) Or ($Nmbr = 31) Or ($Nmbr = 33) Or ($Nmbr = 35) Then
		GUICtrlSetData($Progress4, 5 + Number(GUICtrlRead($Progress4)))
		GUICtrlSetData($Progress3, 0)
		$CurrentBR = $CurrentBR + (2 * $BetOdd)
		GUICtrlSetData($Input2, $CurrentBR)
		$BetOdd = 0
		$BetEven = 0
	EndIf
	If ($Nmbr = 2) Or ($Nmbr = 4) Or ($Nmbr = 6) Or ($Nmbr = 8) Or ($Nmbr = 10) Or ($Nmbr = 12) Or ($Nmbr = 14) Or ($Nmbr = 16) Or ($Nmbr = 18) Or ($Nmbr = 20) Or ($Nmbr = 22) Or ($Nmbr = 24) Or ($Nmbr = 26) Or ($Nmbr = 28) Or ($Nmbr = 30) Or ($Nmbr = 32) Or ($Nmbr = 34) Or ($Nmbr = 36) Then
		GUICtrlSetData($Progress3, 5 + Number(GUICtrlRead($Progress3)))
		GUICtrlSetData($Progress4, 0)
		$CurrentBR = $CurrentBR + (2 * $BetEven)
		GUICtrlSetData($Input2, $CurrentBR)
		$BetOdd = 0
		$BetEven = 0
	EndIf
	If ($Nmbr < 19) And ($Nmbr > 0) Then
		GUICtrlSetData($Progress6, 5 + Number(GUICtrlRead($Progress6)))
		GUICtrlSetData($Progress5, 0)
		$CurrentBR = $CurrentBR + (2 * $Bet1To18)
		GUICtrlSetData($Input2, $CurrentBR)
		$Bet1To18 = 0
		$Bet19To36 = 0
	EndIf
	If ($Nmbr > 18) Then
		GUICtrlSetData($Progress5, 5 + (Number(GUICtrlRead($Progress5))))
		GUICtrlSetData($Progress6, 0)
		$CurrentBR = $CurrentBR + (2 * $Bet19To36)
		GUICtrlSetData($Input2, $CurrentBR)
		$Bet1To18 = 0
		$Bet19To36 = 0
	EndIf
	If ($Nmbr < 13) And ($Nmbr > 0) Then
		GUICtrlSetData($Progress8, 5 + Number(GUICtrlRead($Progress8)))
		GUICtrlSetData($Progress9, 5 + Number(GUICtrlRead($Progress9)))
		GUICtrlSetData($Progress7, 0)
		$CurrentBR = $CurrentBR + (3 * $Bet1stDoz)
		GUICtrlSetData($Input2, $CurrentBR)
		$Bet1stDoz = 0
		$Bet2ndDoz = 0
		$Bet3rdDoz = 0
	EndIf
	If ($Nmbr < 25) And ($Nmbr > 12) Then
		GUICtrlSetData($Progress7, 5 + Number(GUICtrlRead($Progress7)))
		GUICtrlSetData($Progress9, 5 + Number(GUICtrlRead($Progress9)))
		GUICtrlSetData($Progress8, 0)
		$CurrentBR = $CurrentBR + (3 * $Bet2ndDoz)
		GUICtrlSetData($Input2, $CurrentBR)
		$Bet1stDoz = 0
		$Bet2ndDoz = 0
		$Bet3rdDoz = 0
	EndIf
	If ($Nmbr > 24) Then
		GUICtrlSetData($Progress8, 5 + Number(GUICtrlRead($Progress8)))
		GUICtrlSetData($Progress7, 5 + Number(GUICtrlRead($Progress7)))
		GUICtrlSetData($Progress9, 0)
		$CurrentBR = $CurrentBR + (3 * $Bet3rdDoz)
		GUICtrlSetData($Input2, $CurrentBR)
		$Bet1stDoz = 0
		$Bet2ndDoz = 0
		$Bet3rdDoz = 0
	EndIf
	If ($Nmbr = 1) Or ($Nmbr = 4) Or ($Nmbr = 7) Or ($Nmbr = 10) Or ($Nmbr = 13) Or ($Nmbr = 16) Or ($Nmbr = 19) Or ($Nmbr = 22) Or ($Nmbr = 25) Or ($Nmbr = 28) Or ($Nmbr = 31) Or ($Nmbr = 34) Then
		GUICtrlSetData($Progress11, 5 + Number(GUICtrlRead($Progress11)))
		GUICtrlSetData($Progress12, 5 + Number(GUICtrlRead($Progress12)))
		GUICtrlSetData($Progress10, 0)
		$CurrentBR = $CurrentBR + (3 * $BetRow1)
		GUICtrlSetData($Input2, $CurrentBR)
		$BetRow1 = 0
		$BetRow2 = 0
		$BetRow3 = 0
	EndIf
	If ($Nmbr = 2) Or ($Nmbr = 5) Or ($Nmbr = 8) Or ($Nmbr = 11) Or ($Nmbr = 14) Or ($Nmbr = 17) Or ($Nmbr = 20) Or ($Nmbr = 23) Or ($Nmbr = 26) Or ($Nmbr = 29) Or ($Nmbr = 32) Or ($Nmbr = 35) Then
		GUICtrlSetData($Progress10, 5 + Number(GUICtrlRead($Progress10)))
		GUICtrlSetData($Progress12, 5 + Number(GUICtrlRead($Progress12)))
		GUICtrlSetData($Progress11, 0)
		$CurrentBR = $CurrentBR + (3 * $BetRow2)
		GUICtrlSetData($Input2, $CurrentBR)
		$BetRow1 = 0
		$BetRow2 = 0
		$BetRow3 = 0
	EndIf

	;*********Process if Row 3 *****************************
	If ($Nmbr = 3) Or ($Nmbr = 6) Or ($Nmbr = 9) Or ($Nmbr = 12) Or ($Nmbr = 15) Or ($Nmbr = 18) Or ($Nmbr = 21) Or ($Nmbr = 24) Or ($Nmbr = 27) Or ($Nmbr = 30) Or ($Nmbr = 33) Or ($Nmbr = 36) Then
		GUICtrlSetData($Progress10, 5 + Number(GUICtrlRead($Progress10)))
		GUICtrlSetData($Progress11, 5 + Number(GUICtrlRead($Progress11)))
		GUICtrlSetData($Progress12, 0)
		$CurrentBR = $CurrentBR + (3 * $BetRow3)
		GUICtrlSetData($Input2, $CurrentBR)
		$BetRow1 = 0
		$BetRow2 = 0
		$BetRow3 = 0
	EndIf

	;************** Set Tool tips to display how many times a Group HAS NOT come up *****************
	;$Dummy = "Not Seen For " + (GUICtrlRead($Progress2) / 5) + "Spins"
	GUICtrlSetTip($Progress1, GUICtrlRead($Progress1) / 5)
	GUICtrlSetTip($Progress2, GUICtrlRead($Progress2) / 5)
	GUICtrlSetTip($Progress3, GUICtrlRead($Progress3) / 5)
	GUICtrlSetTip($Progress4, GUICtrlRead($Progress4) / 5)
	GUICtrlSetTip($Progress5, GUICtrlRead($Progress5) / 5)
	GUICtrlSetTip($Progress6, GUICtrlRead($Progress6) / 5)
	GUICtrlSetTip($Progress7, GUICtrlRead($Progress7) / 5)
	GUICtrlSetTip($Progress8, GUICtrlRead($Progress8) / 5)
	GUICtrlSetTip($Progress9, GUICtrlRead($Progress9) / 5)
	GUICtrlSetTip($Progress10, GUICtrlRead($Progress10) / 5)
	GUICtrlSetTip($Progress11, GUICtrlRead($Progress11) / 5)
	GUICtrlSetTip($Progress12, GUICtrlRead($Progress12) / 5)

	;Local $iIdleTime = _Timer_GetIdleTime()
	;GUICtrlSetData($Input3, $iIdleTime)

	;****** If Current, suggested Betsize > required Stop loss ten
	If $BetSize >= GUICtrlRead($Input4) Then
		$NewTargetBR = Number(GUICtrlRead($Input2))
		GUICtrlSetData($Input6, $NewTargetBR)
		$BetSize = 1
		GUICtrlSetData($Input7, $BetSize)
	EndIf
	If Number(GUICtrlRead($Input2)) > Number(GUICtrlRead($Input6)) Then
		$MaxBR = Number(GUICtrlRead($Input2))
		GUICtrlSetData($Input6, $MaxBR)
		$BetSize = 1
	EndIf
	$CurrentBR = Number(GUICtrlRead($Input2))
	$NewTargetBR = Number(GUICtrlRead($Input6))
	$BetSize = $NewTargetBR - $CurrentBR
	If $BetSize < 1 Then
		$BetSize = 1
	EndIf
	GUICtrlSetData($Input7, $BetSize)
EndFunc

Func Threshold()
$Threshld = Number( GUICtrlRead ($Input3))
$BetAmount = 0

If ( GUICtrlRead($Checkbox1) = 1) Then  ; If Grp is checked)
If ($CurrentBR > $BetSize) And (GUICtrlRead($Progress1)/5 >= $Threshld) Then
$BetRed = $BetSize
$BetAmount = $BetAmount + $BetSize
Call ("BankRoll")
EndIf
EndIf

If ( GUICtrlRead($Checkbox1) = 1) Then  ; If Grp is checked)
If ($CurrentBR > $BetSize) And (GUICtrlRead($Progress2)/5 >= $Threshld) Then
$BetBlack = $BetSize
$BetAmount = $BetAmount + $BetSize
Call ("BankRoll")
EndIf
EndIf

If ( GUICtrlRead($Checkbox2) = 1) Then  ; If Grp is checked)
If ($CurrentBR > $BetSize) And (GUICtrlRead($Progress3)/5 >= $Threshld) Then
$BetOdd = $BetSize
$BetAmount = $BetAmount + $BetSize
Call ("BankRoll")
EndIf
EndIf

If ( GUICtrlRead($Checkbox2) = 1) Then  ; If Grp is checked)
If ($CurrentBR > $BetSize) And (GUICtrlRead($Progress4)/5 >= $Threshld) Then
$BetEven = $BetSize
$BetAmount = $BetAmount + $BetSize
Call ("BankRoll")
EndIf
EndIf

If ( GUICtrlRead($Checkbox3) = 1) Then  ; If Grp is checked)
If ($CurrentBR > $BetSize) And (GUICtrlRead($Progress5)/5 >= $Threshld) Then
$Bet1To18 = $BetSize
$BetAmount = $BetAmount + $BetSize
Call ("BankRoll")
EndIf
EndIf

If ( GUICtrlRead($Checkbox3) = 1) Then  ; If Grp is checked)
If ($CurrentBR > $BetSize) And (GUICtrlRead($Progress6)/5 >= $Threshld) Then
$Bet19To36 = $BetSize
$BetAmount = $BetAmount + $BetSize
Call ("BankRoll")
EndIf
EndIf

If ( GUICtrlRead($Checkbox4) = 1) Then  ; If Grp is checked)
If ($CurrentBR > $BetSize) And (GUICtrlRead($Progress7)/5 >= $Threshld) Then
$Bet1stDoz = $BetSize
$BetAmount = $BetAmount + $BetSize
Call ("BankRoll")
EndIf
EndIf

If ( GUICtrlRead($Checkbox4) = 1) Then  ; If Grp is checked)
If ($CurrentBR > $BetSize) And (GUICtrlRead($Progress8)/5 >= $Threshld) Then
$Bet2ndDoz = $BetSize
$BetAmount = $BetAmount + $BetSize
Call ("BankRoll")
EndIf
EndIf

If ( GUICtrlRead($Checkbox4) = 1) Then  ; If Grp is checked)
If ($CurrentBR > $BetSize) And (GUICtrlRead($Progress9)/5 >= $Threshld) Then
$Bet3rdDoz = $BetSize
$BetAmount = $BetAmount + $BetSize
Call ("BankRoll")
EndIf
EndIf

If ( GUICtrlRead($Checkbox5) = 1) Then  ; If Grp is checked)
If ($CurrentBR > $BetSize) And (GUICtrlRead($Progress10)/5 >= $Threshld) Then
$BetRow1 = $BetSize
$BetAmount = $BetAmount + $BetSize
Call ("BankRoll")
EndIf
EndIf

If ( GUICtrlRead($Checkbox5) = 1) Then  ; If Grp is checked)
If ($CurrentBR > $BetSize) And (GUICtrlRead($Progress11)/5 >= $Threshld) Then
$BetRow2 = $BetSize
$BetAmount = $BetAmount + $BetSize
Call ("BankRoll")
EndIf
EndIf

If ( GUICtrlRead($Checkbox5) = 1) Then  ; If Grp is checked)
If ($CurrentBR > $BetSize) And (GUICtrlRead($Progress12)/5 >= $Threshld) Then
$BetRow3 = $BetSize
$BetAmount = $BetAmount + $BetSize
Call ("BankRoll")
EndIf
EndIf

;MsgBox($MB_SYSTEMMODAL,"Title", $BetAmount, 20)
;MsgBox($MB_SYSTEMMODAL, "Title", "This message box will timeout after 10 seconds or select the OK button.", 10)

EndFunc

Func BankRoll()
	If $CurrentBR >= $BetSize Then

	$CurrentBR = $CurrentBR - $BetSize
	If ($CurrentBR < 1) Then
		$CurrentBR = 0

	EndIf
	EndIf
	GUICtrlSetData($Input2, $CurrentBR)
	Return
EndFunc   ;==>BankRoll




;*******************************************************
;*******************************************************
;*******************************************************
