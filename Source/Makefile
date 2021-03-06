export MODNAME		:= ExtraplanetaryLaunchpads
export KSPDIR		:= ${HOME}/ksp/KSP_linux
export MANAGED		:= ${KSPDIR}/KSP_Data/Managed
export GAMEDATA		:= ${KSPDIR}/GameData
export MODGAMEDATA	:= ${GAMEDATA}/${MODNAME}
export PLUGINDIR	:= ${MODGAMEDATA}/Plugins

TARGETS		:= bin/Launchpad.dll

EL_FILES := \
	CommandSeat/ControlReference.cs		\
	CommandSeat/FixSeatName.cs			\
	CommandSeat/NoControlSwitch.cs		\
	Converter/Converter.cs				\
	Converter/CoreHeat.cs				\
	Converter/Extractor.cs				\
	Converter/IResourceProvider.cs		\
	Converter/KethaneResourceProvider.cs\
	Converter/StockResourceProvider.cs	\
	DisposablePad/DisposablePad.cs		\
	Hull/Box.cs							\
	Hull/Connectivity.cs				\
	Hull/CraftHull.cs					\
	Hull/Quickhull.cs					\
	Hull/Edge.cs						\
	Hull/FaceSet.cs						\
	Hull/RawMesh.cs						\
	Hull/Triangle.cs					\
	Recipes/BuildCost.cs				\
	Recipes/BuildResource.cs			\
	Recipes/BuildResourceSet.cs			\
	Recipes/ConverterRecipe.cs			\
	Recipes/CostReport.cs				\
	Recipes/Ingredient.cs				\
	Recipes/PartRecipe.cs				\
	Recipes/Recipe.cs					\
	Recipes/RecipeResourceContainer.cs	\
	Recipes/RecipeDatabase.cs			\
	Recipes/RecipeLoader.cs				\
	ResourceManager/IResourceContainer.cs		\
	ResourceManager/KISResourceContainer.cs		\
	ResourceManager/PartResourceContainer.cs	\
	ResourceManager/ResourceInfo.cs				\
	ResourceManager/ResourceManager.cs			\
	ResourceManager/ResourceSet.cs				\
	ResourceManager/ResourceSetContainer.cs		\
	Survey/Billboard.cs					\
	Survey/Points.cs					\
	Survey/SiteBody.cs					\
	Survey/SiteList.cs					\
	Survey/SurveySite.cs				\
	Survey/SurveySkill.cs				\
	Survey/SurveyStake.cs				\
	Survey/SurveyStation.cs				\
	Survey/SurveyTracker.cs				\
	Survey/VirtualPad.cs				\
    assembly/AssemblyInfo.cs			\
	assembly/Checkers.cs				\
	assembly/VersionReport.cs			\
	GUI/BuildWindow.cs					\
	GUI/CraftBrowser.cs					\
	GUI/DropDownList.cs					\
	GUI/EditorToolbar.cs				\
	GUI/ProgressBar.cs					\
	GUI/RenameWindow.cs					\
	GUI/ResourceWindow.cs				\
	GUI/ScrollView.cs					\
	GUI/ShipInfo.cs						\
	GUI/Styles.cs						\
	GUI/TextField.cs					\
	LaunchClamp/LaunchClamp.cs			\
	Pad/Launchpad.cs					\
	Recycler/Recycler.cs				\
	Recycler/StateMachine.cs			\
	Target/Target.cs					\
	Workshop/ConstructionSkill.cs		\
	Workshop/ProtoWorkSink.cs			\
	Workshop/VesselWorkNet.cs			\
	Workshop/WorkSink.cs				\
	Workshop/WorkSource.cs				\
	Workshop/Workshop.cs				\
	lib/KASWrapper.cs					\
	lib/KISWrapper.cs					\
	lib/KACWrapper.cs					\
	lib/KerbalStatsWrapper.cs			\
	lib/Utils.cs						\
	toolbar/Toolbar.cs					\
	toolbar/ToolbarWrapper.cs			\
	AirstreamShield.cs					\
	BuildControl.cs						\
	ControlInterface.cs					\
	Settings.cs							\
	$e

RESGEN2		:= resgen2
GMCS		:= mcs
GMCSFLAGS	:= -optimize -warnaserror -debug
GIT			:= git
TAR			:= tar
ZIP			:= zip

all: version ${TARGETS}

.PHONY: version
version:
	@../tools/git-version.sh

info:
	@echo "${MODNAME} Build Information"
	@echo "    resgen2:    ${RESGEN2}"
	@echo "    gmcs:       ${GMCS}"
	@echo "    gmcs flags: ${GMCSFLAGS}"
	@echo "    git:        ${GIT}"
	@echo "    tar:        ${TAR}"
	@echo "    zip:        ${ZIP}"
	@echo "    KSP Data:   ${KSPDIR}"

bin/Launchpad.dll: ${EL_FILES}
	@mkdir -p bin
	${GMCS} ${GMCSFLAGS} -t:library -lib:${MANAGED} \
		-r:Assembly-CSharp,Assembly-CSharp-firstpass \
		-r:UnityEngine \
		-r:UnityEngine.UI \
		-r:UnityEngine.UIModule \
		-r:UnityEngine.IMGUIModule \
		-r:UnityEngine.TextRenderingModule \
		-r:UnityEngine.AnimationModule \
		-r:UnityEngine.CoreModule \
		-r:UnityEngine.PhysicsModule \
		-r:UnityEngine.InputLegacyModule \
		-out:$@ $^

clean:
	rm -f ${TARGETS}* assembly/AssemblyInfo.cs bin/${MODNAME}.version
	test -d bin && rmdir bin || true

install: all
	mkdir -p ${PLUGINDIR}
	cp ${TARGETS} bin/${MODNAME}.version ${PLUGINDIR}

.PHONY: all clean install
