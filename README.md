//----------------------------------------------------------------------------//
//                                                                            //
//   This material contains, and is a part of a computer software program     //
//   which is, proprietary and confidential information owned by:             //
//                  Honeywell Technologies Solution Lab, INC.                 //
//   The program, including this material, may not be duplicated, disclosed   //
//   or reproduced in whole or in part for any purpose without the express    //
//   written authorization of Honeywell.  All authorized                      //
//   reproductions must be marked with this legend.                           //
//                                                                            //
//              © 2006 Honeywell Technologies Solution Lab, Inc.              //
//              Honeywell Technologies Solution Lab, Incorporated             //
//                            All rights reserved.                            //
//                                                                            //
//----------------------------------------------------------------------------//
//
//    MODULE NAME       :   Util.h
//
//    DESCRIPTIVE NAME  :   Util.h
//
//    MODULE FUNCTION   :   It is used to define constants, enums, maps etc for the application
//
//    MODULE AUTHOR     :   Ashish Negi
//
//    DATE MODULE WRITTEN:  07/24/2006
//
//----------------------------------------------------------------------------
//
//
// History:
// 
//
#ifndef __VNET_UTIL_HeaderFile__
#define __VNET_UTIL_HeaderFile__

#ifndef NCollection_DefineList_HeaderFile
#include <NCollection_DefineList.hxx>
#endif //NCollection_DefineList_HeaderFile

#ifndef NCollection_DefineDataMap_HeaderFile
#include <NCollection_DefineDataMap.hxx>
#endif //NCollection_DefineDataMap_HeaderFile

#ifndef __NCollection_DefineDataMap_HeaderFile__
#include <NCollection_DefineMap.hxx>
#endif //__NCollection_DefineDataMap_HeaderFile__

#include <NCollection_DefineSequence.hxx>

#ifndef _TCollection_AsciiString_HeaderFile
#include <TCollection_AsciiString.hxx> 
#endif //_TCollection_AsciiString_HeaderFile

#include <HFWDataSet/HFWDataRow.hpp>
#include <VNetUtil.h>

#ifndef _Standard_Integer_HeaderFile
#include <Standard_Integer.hxx>
#endif

#ifndef _TColStd_ListOfReal_HeaderFile
#include <TColStd_ListOfReal.hxx>
#endif _TColStd_ListOfReal_HeaderFile

#ifndef _TColStd_ListOfInteger_HeaderFile
#include <TColStd_ListOfInteger.hxx>
#endif _TColStd_ListOfInteger_HeaderFile

#ifndef _TColStd_ListIteratorOfListOfInteger_HeaderFile
#include <TColStd_ListIteratorOfListOfInteger.hxx>
#endif _TColStd_ListIteratorOfListOfInteger_HeaderFile

#ifndef _TColStd_ListIteratorOfListOfReal_HeaderFile
#include <TColStd_ListIteratorOfListOfReal.hxx>
#endif _TColStd_ListIteratorOfListOfReal_HeaderFile

#ifndef _TColStd_Array2OfReal_HeaderFile
#include <TColStd_Array2OfReal.hxx>
#endif _TColStd_Array2OfReal_HeaderFile

#ifndef __HFWVizColor_HeaderFile__
#include <HFWVizColor.hpp>
#endif //__HFWVizColor_HeaderFile__

#include "VNET_1_0_ExportMacros.h"

#include <map>
#include <vector>
#include <iterator>


//DEFINE_BASECOLLECTION(BaseCollectionStringList,TCollection_AsciiString)

//DEFINE_BASECOLLECTION(BaseCollectionBooleanList,Standard_Boolean)
DEFINE_LIST(StringList,BaseCollectionStringList,TCollection_AsciiString)

//DEFINE_BASECOLLECTION(BaseCollectionStringSeq,TCollection_AsciiString)

DEFINE_SEQUENCE(StringSequence,BaseCollectionStringSeq,TCollection_AsciiString)
DEFINE_SEQUENCE(StringSeqSequence, BaseCollectionStringSeqSeq, StringSequence)

DEFINE_DATAMAP(MapOfStringString, BaseCollectionStringList, TCollection_AsciiString, TCollection_AsciiString)
DEFINE_DATAMAP(MapOfBooleanString, BaseCollectionBooleanList, TCollection_AsciiString, Standard_Boolean)

DEFINE_DATAMAP(MapOfStringStringSeq, BaseCollectionStringList, TCollection_AsciiString, StringSequence)

DEFINE_DATAMAP(DMapOfStringStringDMap, BaseCollectionStringList, TCollection_AsciiString, MapOfStringString)

//DEFINE_BASECOLLECTION( BaseCollectionDataRow, Ptr( HFWDataRow))

DEFINE_DATAMAP( MapOfStringDataRow, BaseCollectionDataRow, TCollection_AsciiString, Ptr( HFWDataRow))

//DEFINE_BASECOLLECTION(BaseCollectionStringMap, TCollection_AsciiString)

DEFINE_MAP(MapOfString,BaseCollectionStringMap,TCollection_AsciiString) 

DEFINE_DATAMAP(MapOfStringStringMap, BaseCollectionStringList, TCollection_AsciiString, MapOfString)

DEFINE_DATAMAP(MapOfStringAndStringStringDataMap, BaseCollectionStringList, TCollection_AsciiString, MapOfStringStringMap)

//DEFINE_BASECOLLECTION(BaseCollectionListReal, TColStd_ListOfReal)
DEFINE_DATAMAP(MapOfRealRealList, BaseCollectionListReal, TCollection_AsciiString, TColStd_ListOfReal)
DEFINE_SEQUENCE(SeqOfRealList,BaseCollectionListReal,TColStd_ListOfReal)

DEFINE_DATAMAP(MapOfStringInteger, BaseCollectionStringList, TCollection_AsciiString, Standard_Integer)

//DEFINE_BASECOLLECTION(BaseCollectionListInteger, TColStd_ListOfInteger)
DEFINE_SEQUENCE(SeqOfListInteger, BaseCollectionListInteger,TColStd_ListOfInteger)
//DEFINE_BASECOLLECTION(BaseCollectionSeqListInteger, SeqOfListInteger)
DEFINE_SEQUENCE(SeqSeqOfListInteger, BaseCollectionSeqListInteger, SeqOfListInteger)

typedef std::map<TCollection_AsciiString,TCollection_AsciiString> NetMap;
typedef MapOfString MapOfFREID;

enum en_NodeType
{
	TOP_ELEMENT,//0
	LEVEL1,//1
	SM,//2
	FMEA,//3
	TS,//4
	DP,//5
	ODP,//6
	OP_INSTANCE,//7
	FMEA_INSTANCE,//8
	TS_INSTANCE,//9
	TS_FMEA,//10
	TS_FMEA_INSTANCE//11
};

enum en_FlowSectionType
{
	STANDARD_DRILL,
	CIRCLE,
	AXIAL_GAP,
	RADIAL_GAP_DO,
	RADIAL_GAP_DI,
	RADIAL_GAP_DAVG,
	ANNULUS,
	RECTANGLE,
	SQUARE,
	ROUND_END_SLOT,
	ROUND_SLOT_CC,
	ROUND_SLOT_EE,
	ELLIPSE,
	SEMI_CIRCLE,
	CIRCULAR_SECTOR,
	RIGHT_TRAINGLE,
	ISOSCELES_TRIANGLE,
	DH_PERIMETER,
	DH_AREA,
	PERIMETER_AREA,
	PERIMETER_DE,
	STANDARD_TUBE,
	NONSTANDARD_TUBE,
	CIRCULAR_DO_TW,
	CIRCULAR_DI,
	GEOMETRIC_AREA,
	EFFECTIVE_AREA
};

enum en_EntityType
{
	VN_SEC_NODE		= 10,
	AERO_BC			= 15,
	NON_AERO_BC		= 16,
	VN_STATION		= 20,
	VN_FRE_ENTR		= 21,
	VN_FRE_DHL		= 22,
	VN_FRE_DPR		= 23,	
	VN_FRE_LS		= 25,
	VN_FRE_RS		= 26,
	VN_FRE_FS		= 27,
	VN_FRE_TUBE		= 28,
	VN_FRE_ORIF		= 29,
	VN_FRE_PMPG		= 30,
	VN_FRE_MBEND	= 31,
	VN_FRE_SBEND	= 32,
	VN_FRE_FT		= 33,
	VN_FRE_GRAD		= 35,	
	VN_FRE_ABRP		= 40,
	VN_FRE_RORIF	= 42,
	VN_FRE_CORIF	= 45,
	VN_FRE_DC		= 46,
	VN_FRE_TUBEBEND = 47,
	VN_FRE_TOBI     = 48,
	VN_FRE_AFT     = 49,
	VN_PRINT_AREA	= 50,
	VN_PRINT_AREA_NODE = 51,
	VN_FRE_RC = 52,
	VN_FRE_SS = 53,
	VN_FRE_BS = 54
};

enum en_DesignReqType
{
	DR_COOLED_AIRFOIL,
	DR_DISK_CAVITY,
	DR_SEAL_BUFFERED,
	DR_PRES_TEMP
};

enum en_GoalSeekingObjType
{
	GS_FLOW,
	GS_THRUST_LOAD,
	GS_PRESSURE_DROP,
	GS_OTHER_OUTPUT
};

enum en_SolnDispMode
{
	SD_PSW,
	SD_PS,
	SD_WPCT,
	SD_TTF,
	SD_TTREL,
	SD_PT,
	SD_WPPS,
	SD_DPS,
	SD_DTT,
	SD_RESPCTFLW,
	SD_RESFLW,
	SD_ELE,
	SD_NODE,
	SD_ELENODE,
	SD_LEGACYELMNODE,
	SD_ATPSA,
	SD_ATPSF,
	//TODO: Implementing Concentration Plot feature - Added SD_NODECONC, SD_NODEWPPS, SD_NODEWPCT as three new DisplaySolutionMode options
	//Req: VNET-452
	SD_NODECONC,
	SD_NODEWPPS,
	SD_NODEWPCT,
	SD_EFFGAP
};


struct RGBColor 
{
    Standard_Integer    m_Red;
    Standard_Integer    m_Green;
    Standard_Integer    m_Blue;
    RGBColor( Standard_Integer pRed = 0, Standard_Integer pGreen = 0, Standard_Integer pBlue = 0 ) 
	{
        m_Red   = pRed;
        m_Green = pGreen;
        m_Blue  = pBlue;
    }
};

struct Rect
{
	Standard_Real m_Xmin, m_Xmax;
	Standard_Real m_Ymin, m_Ymax;
	Standard_Real m_Zmin, m_Zmax;
	Rect(Standard_Real l_Xmin = 0, Standard_Real l_Xmax = 0,
					Standard_Real l_Ymin = 0, Standard_Real l_Ymax = 0,
					Standard_Real l_Zmin = 0, Standard_Real l_Zmax = 0)
	{
		m_Xmin = l_Xmin;
		m_Xmax = l_Xmax;
		m_Ymin = l_Ymin;
		m_Ymax = l_Ymax;
		m_Zmin = l_Zmin;
		m_Zmax = l_Zmax;
	}
	bool isDefaultRect() { return (m_Xmin==0 && m_Xmax == 0 && m_Ymin == 0 && m_Ymax ==0 && m_Zmin == 0 && m_Zmax == 0); }
};

struct Point
{
	Standard_Real m_X, m_Y, m_Z;
	Point(Standard_Real l_X = 0, Standard_Real l_Y = 0, Standard_Real l_Z = 0)
	{
		m_X = l_X;
		m_Y = l_Y;
		m_Z = l_Z;
	}
};
enum en_OPNumber
{
	ZERO,
	ONE,
	TWO,
	MORE
};

enum en_IngesElementType
{
	INGRESS,
	EGRESS,
	STATIC
};
enum VNetDataConfigFlag
{
	VNetDataConfigFlag_SM,
	VNetDataConfigFlag_Added,
	VNetDataConfigFlag_Deleted,
	VNetDataConfigFlag_Updated,
	VNetDataConfigFlag_FMEA_Added,
	VNetDataConfigFlag_FMEA_Deleted,
	VNetDataConfigFlag_FMEA_Updated,
	VNetDataConfigFlag_Dummy
};

enum en_ScalingType
{
	SCALING_TYPE_NOT_SET,
	SCALING_TYPE_CUSTOM,
	SCALING_TYPE_EFECTIVENESS,
	SCALING_TYPE_RATIO
};

const TCollection_AsciiString SCALING_TYPE_NOT_SET_STR = "Not Set";
const TCollection_AsciiString SCALING_TYPE_CUSTOM_STR = "Custom";
const TCollection_AsciiString SCALING_TYPE_EFECTIVENESS_STR = "Effectiveness";
const TCollection_AsciiString SCALING_TYPE_RATIO_STR = "Ratio";

enum en_BC_VariationType
{
	PRESSURE,
	TEMPERATURE,
	DELTAP
};
#define FMEAFRETHICKNESS				4
#define SMTSFRETHICKNESS				1

#define UNKNOWNOP						"Unknown OperatingPoint"
#define UNKNOWNOPNAME					"Unknown OperatingPoint"
#define DESIGNPT						"Design Point"
#define OFFDESIGNPT						"Off Design Point"
#define STATUSMODEL						"Status Model"
#define FAILUREMODE						"FMEA"
#define TRADESTUDY						"Trade Study"
#define TRADESTUDYFMEA					"Trade Study FMEA"
#define DEFAULTPHASE					"Testing And Validation"


#define FRE_FACESEAL					"Face Seal"
#define FRE_LABYRINTHSEAL				"Labyrinth Seal"
#define FRE_RINGSEAL					"Ring Seal"
#define FRE_ORIFICE						"Orifice"
#define	FRE_RORIF						"RORIF"
#define	FRE_CORIF						"CORIF"
#define	FRE_TOBI						"Tobi"
#define FRE_TUBE						"Tube"
#define FRE_DISKCAVITY					"Disk Cavity"
#define FRE_ENTRANCE					"Entrance"
#define FRE_SBEND						"SBEND"
#define FRE_MBEND						"MBEND"
#define FRE_DHL							"DHL"
#define FRE_DPR							"DPR"
#define FRE_ABRP						"ABRP"
#define FRE_GRAD						"GRAD"
#define FRE_TUBEBEND					"TUBEBEND"
#define FRE_FT							"FT"
#define FRE_RC							"Re-circulation"
#define FRE_SS							"Static Seal"
#define FRE_BRUSHSEAL					"Brush Seal"
#define FRE_AIRPIN                      "Airpin"

// Labyrinth Seal 
#define TOOTH_RADIUS					"ToothRadius"
#define TOOTH_PITCH						"ToothPitch"
#define TOOTH_STEP						"ToothStep"
#define TOOTH_COUNT						"ToothCount"
#define LAND_MATERIAL					"LandMaterial"
#define INLET_RADIUS					"InletRadius"
#define EXIT_RADIUS						"ExitRadius"
#define INLET_LOSS						"InletLoss"
#define RADIUS							"Radius"
#define LENGTH							"Length"
#define SEAL_TILT						"SealTilt"
#define FSGEOMNOTES						"FSGeomNotes"
#define LSGEOMNOTES						"LSGeomNotes"
#define RSGEOMNOTES						"RSGeomNotes"
#define BSGEOMNOTES						"BSGeomNotes"
#define RUNN_CLR_NOTES					"SealRunnClrNotes"
#define HT_NOTES						"HeatTransferNotes"
#define DESIGN_POINT					"DesignOperatingPoint"
#define OFF_DESIGN_POINT				"OffDesignOperatingPoint"
#define ODP_RUNNCLEARANCE				"OffDesignPtRunnClearance"
#define DP_RUNNCLEARANCE				"DesignPtRunnClearance"
#define DELTA_CLEARANCE					"DeltaClearance"
#define RESULTANT_RUNNCLEARANCE			"ResultantRunningClearance"
#define	HT_OFF_DESIGN_POINT				"HTOffDesignOperatingPoint"
#define HT_DESIGN_POINT					"HTDesignOperatingPoint"
#define ODP_HEAT_TRANSFER				"OffDesignHeatTransfer"
#define DP_HEAT_TRANSFER				"DesignPtHeatTransfer"
#define HT_CORRECTION					"HeatTransferCorrection"
#define RESULTANT_HEATTRANSFER          "ResultantHeatTransfer"
#define FLOW_ELE_DESCRIPTION			"FlowElementDescription"
#define THERMALNOTES					"ThermalNotes"
#define HT_CORRECTIONTYPE               "HeatTransferCorrectionType"

#define SS_TYPE							"Type"
#define SS_DIAMETER						"Diameter"
#define SS_SEALING_SURFACE				"SealingSurfaces"
#define SS_GEOM_NOTES					"SSGeomNotes"
#define SS_FRIC_FACT					"FrictionFactorCorr"
#define SS_CONVOLUTE					"Convolute"
#define SS_ROUGHNES                     "Roughness"
#define SS_COMPRESSION                  "Compression"
#define SS_USERDEFGAP					"UserDefinedGap"
#define SS_FRIC_FACT_NOTES				"FrictionFactorNote"



//Tube Orif 

#define FA2_FLOWSECTION			        "FA2FlowSectionType"
#define FA2_QUANTITY					"FA2Quantity"
#define FA2_PARAMETER1			        "FA2Parameter1"
#define FA2_PARAMETER2			        "FA2Parameter2"
#define FA2_FLOWAREANOTES		        "FA2FloAreaNotes"
#define FA_FLOWSECTION			        "FlowSectionType"
#define FA_QUANTITY 					"Quantity"
#define FA_PARAMETER1			        "Parameter1"
#define FA_PARAMETER2			        "Parameter2"
#define FA_FLOWAREANOTES		        "FloAreaNotes"
#define MA_FLOWSECTION			        "MAFlowSectionType"
#define MA_QUANTITY						"MAQuantity"
#define MA_PARAMETER1			        "MAParameter1"
#define MA_PARAMETER2			        "MAParameter2"
#define MA_FLOWAREANOTES		        "MAFloAreaNotes"


#define FRICTIONFACTORCORR              "FrictionFactorCorr"
#define ENTRANCELOSS                    "EntranceLoss"
#define ROUGHNESSABSOLUTE               "RoughnessAbsolute"
#define FRICTIONLENGTH                  "FrictionLength"
#define REYNOLDNUMBER                   "ReynoldNumber"
#define RELATIVEROUGHNESS               "RelativeRoughness"
#define MOODYFRICTIONFACTOR             "MoodyFrictionFactor"
#define FRICTIONFACTORNOTES             "FrictionFactorNotes"
#define FLOWCOEFFICIENT                 "FlowCoefficient"
#define FLOWCOEFFICIENT_TYPE            "FlowCoefficientType"
#define FLOWCOEFFICIENT_OVERFLOW_TYPE   "FlowCoefficientOverFlowType"
#define TUNINGFACTOR					"TuningFactor"


#define DK_INNER_RAD					"CavityInnerRadius"
#define DK_OUTER_RAD					"CavityOuterRadius"
#define DK_TYPE							"DiskCavityType"
#define DK_APP_SLIP_FACT				"ApparantSlipFactor"
#define DK_SLIP_FACT_TEMP				"SlipFactorTemperature"
#define DK_DISK_SPPED					"DiskSpeed"
#define DK_SHROUD_SPEED					"ShroudSpeed"
#define DK_GEOM_NOTES					"DiskCavGeomNotes"


#define DK_FLODISC_TYPE					"FlowDiscouragerType"
#define DK_RAD_BL_BEGIN					"RadiusBLBegins"
#define DK_PURGE_SCALE_FACT				"PurgeReqScaleFactor"

#define AFT_MODEL_INPUTFILE				"AirpinModelInputFile"
#define AFT_MODEL_QUESTION1			    "AirpinModelQuestion1"
#define AFT_MODEL_NOTES			        "AirpinModelNotes"

#define AFT_FLOWTABLE_INLET				"AirpinFlowTableInlet"
#define AFT_FLOWTABLE_OUTLET		    "AirpinFlowTableOutlet"
#define AFT_FLOWTABLE_QUANTITY		    "AirpinFlowTableQuantity"
#define AFT_FLOWTABLE_SUSPEND			"AirpinFlowTableSuspend"
#define AFT_FLOWTABLE_NOTES			    "AirpinFlowTableNotes"
#define AFT_FLOWTABLE_PARAMETER1		"AirpinFlowTableParameter1"
#define AFT_FLOWTABLE_PARAMETER2	    "AirpinFlowTableParameter2"
#define AFT_FLOWTABLE_PARAMETER3	    "AirpinFlowTableParameter3"
#define AFT_FLOWTABLE_PARAMETER4	    "AirpinFlowTableParameter4"


#define AFT_AEROBCSCALING_PARAMETER1	"AirpinAeroBCScalingParameter1"
#define AFT_AEROBCSCALING_PARAMETER2	"AirpinAeroBCScalingParameter2"
#define AFT_AEROBCSCALING_PARAMETER3	"AirpinAeroBCScalingParameter3"
#define AFT_AEROBCSCALING_PARAMETER4	"AirpinAeroBCScalingParameter4"
#define AFT_AEROBCSCALING_OPID			"AirpinAeroBCScalingOPID"
#define AFT_AEROBCSCALING_NOTES			"AirpinAeroBCScalingNotes"


#define VARIATION_RBSELECTION			"VariationRadioButtonSelection"
#define VARIATION_FCHLAPPLY				"VariationFCHLApply"
#define VARIATION_SCHLAPPLY				"VariationSCHLApply"
#define VARIATION_TCHLAPPLY				"VariationTCHLApply"
#define VARIATION_4THCHLAPPLY			"Variation4thCHLApply"
#define VARIATION_5THCHLAPPLY			"Variation5thCHLApply"
#define VARIATION_6THCHLAPPLY			"Variation6thCHLApply"
#define VARIATION_DIA_DISTRIBUTION		"VariationDiaDistribution"
#define VARIATION_DIA_SIGQUALITY		"VariationDiaSigmaQuality"
#define VARIATION_DIA_INPUTOPT			"VariationDiaInputOption"
#define VARIATION_DIA_PARA1				"VariationDiaParameter1"
#define VARIATION_DIA_PARA2				"VariationDiaParameter2"
#define VARIATION_DIA_PARA3				"VariationDiaParameter3"
#define VARIATION_DIA_PARA4				"VariationDiaParameter4"
#define VARIATION_DIA_LEFTFOLDENAB		"VariationDiaLeftFoldEnabled"
#define VARIATION_DIA_RIGHTFOLDENAB		"VariationDiaRightFoldEnabled"
#define VARIATION_DIA_LEFTFOLDVALUE		"VariationDiaLeftFoldValue"
#define VARIATION_DIA_RIGHTFOLDVALUE	"VariationDiaRightFoldValue"

#define VARIATION_AG_DISTRIBUTION		"VariationAGDistribution"
#define VARIATION_AG_SIGQUALITY			"VariationAGSigmaQuality"
#define VARIATION_AG_INPUTOPT			"VariationAGInputOption"
#define VARIATION_AG_PARA1				"VariationAGParameter1"
#define VARIATION_AG_PARA2				"VariationAGParameter2"
#define VARIATION_AG_PARA3				"VariationAGParameter3"
#define VARIATION_AG_PARA4				"VariationAGParameter4"
#define VARIATION_AG_LEFTFOLDENAB		"VariationAGLeftFoldEnabled"
#define VARIATION_AG_RIGHTFOLDENAB		"VariationAGRightFoldEnabled"
#define VARIATION_AG_LEFTFOLDVALUE		"VariationAGLeftFoldValue"
#define VARIATION_AG_RIGHTFOLDVALUE		"VariationAGRightFoldValue"

#define VARIATION_FC_DISTRIBUTION		"VariationFCDistribution"
#define VARIATION_FC_SIGQUALITY			"VariationFCSigmaQuality"
#define VARIATION_FC_INPUTOPT			"VariationFCInputOption"
#define VARIATION_FC_PARA1				"VariationFCParameter1"
#define VARIATION_FC_PARA2				"VariationFCParameter2"
#define VARIATION_FC_PARA3				"VariationFCParameter3"
#define VARIATION_FC_PARA4				"VariationFCParameter4"
#define VARIATION_FC_LEFTFOLDENAB		"VariationFCLeftFoldEnabled"
#define VARIATION_FC_RIGHTFOLDENAB		"VariationFCRightFoldEnabled"
#define VARIATION_FC_LEFTFOLDVALUE		"VariationFCLeftFoldValue"
#define VARIATION_FC_RIGHTFOLDVALUE		"VariationFCRightFoldValue"

#define VARIATION_DIA_VARIABLE_NAME		"VariationDiaVariableName"
#define VARIATION_AG_VARIABLE_NAME		"VariationAGVariableName"
#define VARIATION_FC_VARIABLE_NAME		"VariationFCVariableName"

#define VARIATION_4THVAR_DISTRIBUTION		"Variation4thVarDistribution"
#define VARIATION_4THVAR_SIGQUALITY			"Variation4thVarSigmaQuality"
#define VARIATION_4THVAR_INPUTOPT			"Variation4thVarInputOption"
#define VARIATION_4THVAR_PARA1				"Variation4thVarParameter1"
#define VARIATION_4THVAR_PARA2				"Variation4thVarParameter2"
#define VARIATION_4THVAR_PARA3				"Variation4thVarParameter3"
#define VARIATION_4THVAR_PARA4				"Variation4thVarParameter4"
#define VARIATION_4THVAR_LEFTFOLDENAB		"Variation4thVarLeftFoldEnabled"
#define VARIATION_4THVAR_RIGHTFOLDENAB		"Variation4thVarRightFoldEnabled"
#define VARIATION_4THVAR_LEFTFOLDVALUE		"Variation4thVarLeftFoldValue"
#define VARIATION_4THVAR_RIGHTFOLDVALUE		"Variation4thVarRightFoldValue"

#define VARIATION_5THVAR_DISTRIBUTION		"Variation5thVarDistribution"
#define VARIATION_5THVAR_SIGQUALITY			"Variation5thVarSigmaQuality"
#define VARIATION_5THVAR_INPUTOPT			"Variation5thVarInputOption"
#define VARIATION_5THVAR_PARA1				"Variation5thVarParameter1"
#define VARIATION_5THVAR_PARA2				"Variation5thVarParameter2"
#define VARIATION_5THVAR_PARA3				"Variation5thVarParameter3"
#define VARIATION_5THVAR_PARA4				"Variation5thVarParameter4"
#define VARIATION_5THVAR_LEFTFOLDENAB		"Variation5thVarLeftFoldEnabled"
#define VARIATION_5THVAR_RIGHTFOLDENAB		"Variation5thVarRightFoldEnabled"
#define VARIATION_5THVAR_LEFTFOLDVALUE		"Variation5thVarLeftFoldValue"
#define VARIATION_5THVAR_RIGHTFOLDVALUE		"Variation5thVarRightFoldValue"

#define VARIATION_6THVAR_DISTRIBUTION		"Variation6thVarDistribution"
#define VARIATION_6THVAR_SIGQUALITY			"Variation6thVarSigmaQuality"
#define VARIATION_6THVAR_INPUTOPT			"Variation6thVarInputOption"
#define VARIATION_6THVAR_PARA1				"Variation6thVarParameter1"
#define VARIATION_6THVAR_PARA2				"Variation6thVarParameter2"
#define VARIATION_6THVAR_PARA3				"Variation6thVarParameter3"
#define VARIATION_6THVAR_PARA4				"Variation6thVarParameter4"
#define VARIATION_6THVAR_LEFTFOLDENAB		"Variation6thVarLeftFoldEnabled"
#define VARIATION_6THVAR_RIGHTFOLDENAB		"Variation6thVarRightFoldEnabled"
#define VARIATION_6THVAR_LEFTFOLDVALUE		"Variation6thVarLeftFoldValue"
#define VARIATION_6THVAR_RIGHTFOLDVALUE		"Variation6thVarRightFoldValue"

#define VARIATION_4TH_VARIABLE_NAME		"Variation4thVariableName"
#define VARIATION_5TH_VARIABLE_NAME		"Variation5thVariableName"
#define VARIATION_6TH_VARIABLE_NAME		"Variation6thVariableName"

#define GSOBJ_INPUT_RBSELECTION			"GSInputRadioButtonSelection"
#define GSOBJ_INPUT_FCHLAPPLY				"GSInputFCHLApply"
#define GSOBJ_INPUT_SCHLAPPLY				"GSInputSCHLApply"
#define GSOBJ_INPUT_TCHLAPPLY				"GSInputTCHLApply"
#define GSOBJ_INPUT_DIA_MINIMUM			"GSInputDiaMinimum"
#define GSOBJ_INPUT_DIA_MAXIMUM			"GSInputDiaMaximum"
#define GSOBJ_INPUT_DIA_RELAX			"GSInputDiaRelax"
#define GSOBJ_INPUT_DIA_ERROR				"GSInputDiaError"

#define GSOBJ_INPUT_AG_MINIMUM		"GSInputAGMinimum"
#define GSOBJ_INPUT_AG_MAXIMUM			"GSInputAGMaximum"
#define GSOBJ_INPUT_AG_RELAX			"GSInputAGRelax"
#define GSOBJ_INPUT_AG_ERROR				"GSInputAGError"

#define GSOBJ_INPUT_FC_MINIMUM		"GSInputFCMinimum"
#define GSOBJ_INPUT_FC_MAXIMUM			"GSInputFCMaximum"
#define GSOBJ_INPUT_FC_RELAX			"GSInputFCRelax"
#define GSOBJ_INPUT_FC_ERROR				"GSInputFCError"

#define GSOBJ_INPUT_DIA_VARIABLE_NAME		"GSInputDiaVariableName"
#define GSOBJ_INPUT_AG_VARIABLE_NAME		"GSInputAGVariableName"
#define GSOBJ_INPUT_FC_VARIABLE_NAME		"GSInputFCVariableName"



#define CHAR_LIST						"abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ\\|=+_)(*&^%$#@!~<,?'"
#define CHAR_LIST_TEMP					"abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ\\|=+_)(*&^%$#@!~<,?' "



#define SM_CLR			HFWVizColor_GREEN
#define FMEA_CLR		HFWVizColor_BLUE1
#define TS_CLR			HFWVizColor_BLUE1
#define TS_FMEA_CLR		HFWVizColor_BLUE1
#define UPDATE_CLR		HFWVizColor_RED
#define DELETE_CLR		HFWVizColor_MATRAGRAY
#define DUMMYFRE_CLR	HFWVizColor_ORANGE
#define DUMMYNODE_CLR	HFWVizColor_ORANGE






#define MESH_LOOP_OVERLAP_ERROR "Loop can not be overlapped"
#define MESH_LOOP_FORMED_ERROR "  Loop has been formed.   "	
#define MESH_CONS_NODES_LIMIT_ERROR "Snap two points to the upper blue line.\nDrag a point above the line and release.\n\nSnap two points to the lower blue line.\nDrag a point below the line and release."
#define MESH_THROUGH_FLOW_ERROR " Through flow property is violated."
#define MESH_DISK_IDENTIFICATION_ERROR " Disk has not been identified.\nDo you want to identify disk?"
#define MESH_LOOP_MESHED_ERROR " Loop is already meshed."
#define MESH_EXTREME_NODE_ERROR "Points at inner and outer radii are fixed when red mesh lines are present.\nDo you want red mesh lines removed?"
#define MESH_NODE_ALTER_ERROR "Mesh Node can not be altered.\nFirst disable the ZRef and Reference Line."
#define MESH_NODE_ADD_ERROR "Can not add the node.\nOnly two consecutive Nodes should be there at each limit"
#define MESH_EDGE_DELETE_ERROR "Edge can not be deleted during meshing."
#define MESH_NODE_DELETE_ERROR "Node can not be deleted as it is shared by the edges."
#define MESH_DISK_NOT_IDENTIFIED_ERROR "Disk has not been identified"
#define MESH_MESHING_NOT_DONE_ERROR "Meshing has not been done."

#define REC_DELETED "RecordDeleted"
//colors for nodes and FREs
/*
HFWVizColor	g_colorBCNode = HFWVizColor_PINK;
HFWVizColor	g_colorAeroBCNode = HFWVizColor_SKYBLUE;
HFWVizColor	g_colorFRE = HFWVizColor_GREEN;
*/
#define BCNODE_CLR HFWVizColor_GREEN
#define AEROBCNODE_CLR HFWVizColor_GREEN
#define FRE_CLR HFWVizColor_GREEN


#define     GRAPHIC_FACTORY    "VNetGraphics"

#define APPCOLOR RGB(236,239,244)

#define AOVOUTPUTFILENAME "variation_AOV.csv"

#define VNetLogger HFWLogger
#define VN_LOG_WARN HFW_LOG_WARN
#define VN_LOG_DEBUG HFW_LOG_DEBUG
#define VN_LOG_INFO	HFW_LOG_INFO
#define VN_LOG_WARN	HFW_LOG_WARN
#define VN_LOG_ERROR HFW_LOG_ERROR

const TCollection_AsciiString STR_NODE("Node");
const TCollection_AsciiString STR_LOCATION("Location");
const TCollection_AsciiString STR_PARAMETER("Parameter");
const TCollection_AsciiString STR_FUNCTION("Function");
const TCollection_AsciiString STR_SCALING_FUNCTION("ScalingFunction");
const TCollection_AsciiString STR_SCALING_GROUPNAME("ScalingGroupName");
const TCollection_AsciiString STR_NODE_NUMBER("NodeNumber");
const TCollection_AsciiString STR_NODE_LOCATION("NodeLocation");
const TCollection_AsciiString STR_PS_PARAM("Ps (psi)");
const TCollection_AsciiString STR_TT_PARAM("Tt (F)");
const TCollection_AsciiString STR_SCALING_FUNCTIONTYPE("ScalingFunctionType");
const TCollection_AsciiString STR_PS_SCALING_FUNCTION("PsScalingFunction");
const TCollection_AsciiString STR_PS_SCALING_CONSTANT("PsScalingConstant");
const TCollection_AsciiString STR_TT_SCALING_FUNCTION("TtScalingFunction");
const TCollection_AsciiString STR_TT_SCALING_CONSTANT("TtScalingConstant");



class VNET_1_0_EXPORT VNet_Global
{
public:

	static std::map<en_ScalingType, TCollection_AsciiString> g_mapScalingTypeString;	
	static void initializeGlobalStringMaps();

	static Standard_Boolean FindStringInSequence(TCollection_AsciiString& p_strSearchString, StringSequence& p_seqSequenceToBeSearched);
	static Standard_Boolean FindStringinList(TCollection_AsciiString& p_strSearchString, StringList& p_listToBeSearched);
};
#endif//__VNET_UTIL_HeaderFile__
