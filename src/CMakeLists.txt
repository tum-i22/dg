if (LLVM_DG)

add_library(LLVMdg MODULE
           llvm/LLVMNode.cpp
           llvm/LLVMDependenceGraph.cpp
           llvm/LLVMDGVerifier.cpp
           llvm/analysis/PostDominators.cpp
           llvm/analysis/DefUse.cpp
           llvm/MemAllocationFuncs.cpp
           llvm/analysis/PointsTo/PointerSubgraph.cpp
           llvm/analysis/PointsTo/Structure.cpp
           llvm/analysis/PointsTo/Globals.cpp
           llvm/analysis/PointsTo/PointerSubgraphValidator.cpp
           llvm/analysis/ReachingDefinitions/LLVMRDBuilderDense.cpp
           llvm/analysis/ReachingDefinitions/LLVMRDBuilderSemisparse.cpp
           analysis/Offset.cpp
           analysis/ReachingDefinitions/ReachingDefinitions.cpp
           analysis/ReachingDefinitions/RDMap.cpp
           analysis/PointsTo/Pointer.cpp
           analysis/PointsTo/PointerAnalysis.cpp
           analysis/PointsTo/PointerSubgraphValidator.cpp
           llvm/analysis/PointsTo/Calls.cpp
           llvm/analysis/PointsTo/Constants.cpp
           llvm/analysis/PointsTo/Instructions.cpp
           )

target_compile_features(LLVMdg PRIVATE cxx_range_for cxx_auto_type)
set_target_properties(LLVMdg PROPERTIES COMPILE_FLAGS "-std=c++11 -fno-rtti -g")

add_library(LLVMpass MODULE
           FunctionsPass.cpp)

target_compile_features(LLVMpass PRIVATE cxx_range_for cxx_auto_type)
set_target_properties(LLVMpass PROPERTIES COMPILE_FLAGS "-std=c++11 -fno-rtti -g")
#target_link_libraries(LLVMpass "-lLLVMSupport")

if(APPLE)
    set_target_properties(LLVMpass PROPERTIES
            LINK_FLAGS "-undefined dynamic_lookup"
            )
endif(APPLE)


install(TARGETS LLVMdg
	LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR})

install(FILES
       BBlock.h
       DependenceGraph.h
       DGParameters.h
       Node.h
       DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}/llvm-dg)
install(FILES
        ADT/Bits.h
        ADT/Bitvector.h
        ADT/DGContainer.h
        ADT/NumberSet.h
        ADT/Queue.h
	DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}/llvm-dg/ADT/)
install(FILES
    analysis/Analysis.h
    analysis/BFS.h
    analysis/DataFlowAnalysis.h
    analysis/DFS.h
    analysis/NodesWalk.h
    analysis/Offset.h
    analysis/PostDominanceFrontiers.h
    analysis/SCC.h
    analysis/Slicing.h
    analysis/SubgraphNode.h
    DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}/llvm-dg/analysis/)
install(FILES
        analysis/ControlExpression/CENode.h
        analysis/ControlExpression/CFA.h
        analysis/ControlExpression/ControlExpression.h
        DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}/llvm-dg/analysis/ControlExpression)
install(FILES
        analysis/PointsTo/MemoryObject.h
        analysis/PointsTo/PointerAnalysis.h
        analysis/PointsTo/Pointer.h
        analysis/PointsTo/PointerSubgraph.h
        analysis/PointsTo/PointerSubgraphOptimizations.h
        analysis/PointsTo/PointerSubgraphValidator.h
        analysis/PointsTo/PointsToFlowInsensitive.h
        analysis/PointsTo/PointsToFlowSensitive.h
        analysis/PointsTo/PointsToMapping.h
        analysis/PointsTo/PointsToSet.h
        analysis/PointsTo/PointsToWithInvalidate.h
        analysis/PointsTo/PSNode.h
	DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}/llvm-dg/analysis/PointsTo/)
install(FILES
	analysis/ReachingDefinitions/ReachingDefinitions.h
	analysis/ReachingDefinitions/RDMap.h
    analysis/ReachingDefinitions/SemisparseRda.h
	DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}/llvm-dg/analysis/ReachingDefinitions/)
install(FILES
    analysis/ReachingDefinitions/Srg/AssignmentFinder.h
    analysis/ReachingDefinitions/Srg/CytronSRGBuilder.h
    analysis/ReachingDefinitions/Srg/IntervalMap.h
    analysis/ReachingDefinitions/Srg/MarkerSRGBuilderFI.h
    analysis/ReachingDefinitions/Srg/MarkerSRGBuilderFS.h
    analysis/ReachingDefinitions/Srg/PhiPlacement.h
    analysis/ReachingDefinitions/Srg/SparseRDGraphBuilder.h
	DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}/llvm-dg/analysis/ReachingDefinitions/Srg/)
install(FILES
	llvm/llvm-utils.h
	llvm/MemAllocationFuncs.h
    llvm/LLVMDependenceGraph.h
    llvm/LLVMNode.h
    llvm/Slicer.h
	DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}/llvm-dg/llvm/)
install(FILES
	llvm/analysis/DefUse.h
	llvm/analysis/ControlExpression.h
	DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}/llvm-dg/llvm/analysis/)

install(FILES
	llvm/analysis/PointsTo/PointerSubgraph.h
	llvm/analysis/PointsTo/PointsTo.h
    llvm/analysis/PointsTo/PointerSubgraphValidator.h
	DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}/llvm-dg/llvm/analysis/PointsTo/)
install(FILES
	llvm/analysis/ReachingDefinitions/ReachingDefinitions.h
    llvm/analysis/ReachingDefinitions/LLVMRDBuilder.h
    llvm/analysis/ReachingDefinitions/LLVMRDBuilderDense.h
    llvm/analysis/ReachingDefinitions/LLVMRDBuilderSemisparse.h
	DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}/llvm-dg/llvm/analysis/ReachingDefinitions/)


endif(LLVM_DG)
